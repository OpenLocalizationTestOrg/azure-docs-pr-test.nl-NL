---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="3c6eb-101">Verbinding maken met uw Linux-computers tooLog Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="3c6eb-102">Log Analytics gebruikt, kunt u verzamelen en reageren op gegevens die zijn gegenereerd op basis van Linux-computers.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="3c6eb-103">Kunt u gegevens verzameld van Linux tooOMS toe te voegen toomanage Linux-systemen en container-oplossingen zoals Docker, ongeacht de locatie van uw computers: vrijwel elke locatie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="3c6eb-104">Gegevensbronnen mogelijk bevinden zich in uw on-premises datacentrum als fysieke servers en virtuele computers in een cloud-gebaseerde service zoals Amazon Web Services (AWS) of Microsoft Azure, of zelfs Hallo laptop op uw eigen bureau.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="3c6eb-105">Bovendien verzamelt OMS ook gegevens van Windows-computers op dezelfde manier, zodat deze ondersteuning biedt voor een echt hybride IT-omgeving.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="3c6eb-106">U kunt weergeven en beheren van gegevens uit alle bronnen met logboekanalyse in OMS met een één-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="3c6eb-107">Dit vermindert de behoefte aan Hallo toomonitor met behulp van veel verschillende systemen, maakt het eenvoudig tooconsume, en u kunt elke gewenste toowhatever business analytics-oplossing of systeem dat u al hebt gegevens exporteren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="3c6eb-108">Dit artikel is een snelstartgids waarmee u het verzamelen en beheren van gegevens voor uw Linux-computers met behulp van Hallo OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="3c6eb-109">Voor meer technische informatie zoals proxyserverconfiguratie, informatie over CollectD metrische gegevens en aangepaste JSON-gegevensbronnen vindt u die informatie op [OMS-Agent voor Linux-overzicht](https://github.com/Microsoft/OMS-Agent-for-Linux) en [OMS-Agent voor volledige documentatie Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="3c6eb-110">Op dit moment kunt u de volgende soorten gegevens uit Linux-computers Hallo verzamelen:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="3c6eb-111">Maatstaven voor prestaties</span><span class="sxs-lookup"><span data-stu-id="3c6eb-111">Performance metrics</span></span>
* <span data-ttu-id="3c6eb-112">Syslog-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-112">Syslog events</span></span>
* <span data-ttu-id="3c6eb-113">Waarschuwingen van Nagios en Zabbix</span><span class="sxs-lookup"><span data-stu-id="3c6eb-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="3c6eb-114">Maatstaven voor prestaties van docker-container, inventaris en Logboeken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="3c6eb-115">Ondersteunde versies van Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-115">Supported Linux versions</span></span>
<span data-ttu-id="3c6eb-116">X86- en x64 versies worden officieel ondersteund op tal van Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="3c6eb-117">Hallo OMS-Agent voor Linux kan echter ook uitvoeren op andere distributies niet wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="3c6eb-118">Amazon Linux 2012.09 via 2015.09</span><span class="sxs-lookup"><span data-stu-id="3c6eb-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="3c6eb-119">CentOS Linux 5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="3c6eb-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="3c6eb-120">Oracle Linux 5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="3c6eb-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="3c6eb-121">Red Hat Enterprise Linux Server 5, 6 en 7</span><span class="sxs-lookup"><span data-stu-id="3c6eb-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="3c6eb-122">Debian GNU/Linux 6, 7 en 8</span><span class="sxs-lookup"><span data-stu-id="3c6eb-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="3c6eb-123">Ubuntu 12.04 TNS, 14.04 TNS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="3c6eb-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="3c6eb-124">SUSE Linux Enterprise Server 11 en 12</span><span class="sxs-lookup"><span data-stu-id="3c6eb-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="3c6eb-125">OMS-Agent voor Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-125">OMS Agent for Linux</span></span>
<span data-ttu-id="3c6eb-126">Hallo Operations Management Suite-Agent voor Linux bestaat uit meerdere pakketten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="3c6eb-127">Hallo release-bestand bevat hello-pakketten beschikbaar door actieve Hallo shell-bundel met volgende `--extract`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="3c6eb-128">**Pakket**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-128">**Package**</span></span> | <span data-ttu-id="3c6eb-129">**Versie**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-129">**Version**</span></span> | <span data-ttu-id="3c6eb-130">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c6eb-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="3c6eb-131">omsagent</span></span> |<span data-ttu-id="3c6eb-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3c6eb-132">1.1.0</span></span> |<span data-ttu-id="3c6eb-133">Hallo Operations Management Suite-Agent voor Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="3c6eb-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="3c6eb-134">omsconfig</span></span> |<span data-ttu-id="3c6eb-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="3c6eb-135">1.1.1</span></span> |<span data-ttu-id="3c6eb-136">Configuratie-agent voor Hallo OMS-Agent</span><span class="sxs-lookup"><span data-stu-id="3c6eb-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="3c6eb-137">OMI</span><span class="sxs-lookup"><span data-stu-id="3c6eb-137">omi</span></span> |<span data-ttu-id="3c6eb-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="3c6eb-138">1.0.8.3</span></span> |<span data-ttu-id="3c6eb-139">Open Management Infrastructure (OMI)--een lichtgewicht CIM-Server</span><span class="sxs-lookup"><span data-stu-id="3c6eb-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="3c6eb-140">scx</span><span class="sxs-lookup"><span data-stu-id="3c6eb-140">scx</span></span> |<span data-ttu-id="3c6eb-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="3c6eb-141">1.6.2</span></span> |<span data-ttu-id="3c6eb-142">OMI CIM-Providers voor maatstaven voor prestaties van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="3c6eb-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="3c6eb-143">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="3c6eb-143">apache-cimprov</span></span> |<span data-ttu-id="3c6eb-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3c6eb-144">1.0.0</span></span> |<span data-ttu-id="3c6eb-145">Apache HTTP-Server prestatiebewaking-provider voor OMI.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3c6eb-146">Alleen geïnstalleerd als de Apache HTTP-Server wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="3c6eb-147">MySQL-cimprov</span><span class="sxs-lookup"><span data-stu-id="3c6eb-147">mysql-cimprov</span></span> |<span data-ttu-id="3c6eb-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3c6eb-148">1.0.0</span></span> |<span data-ttu-id="3c6eb-149">MySQL-Server prestatiebewaking-provider voor OMI.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3c6eb-150">Alleen geïnstalleerd als MySQL/MariaDB server wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="3c6eb-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="3c6eb-151">docker-cimprov</span></span> |<span data-ttu-id="3c6eb-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="3c6eb-152">0.1.0</span></span> |<span data-ttu-id="3c6eb-153">Docker-provider voor OMI.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-153">Docker provider for OMI.</span></span> <span data-ttu-id="3c6eb-154">Alleen geïnstalleerd als Docker wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="3c6eb-155">Aanvullende installatie-artefacten</span><span class="sxs-lookup"><span data-stu-id="3c6eb-155">Additional installation artifacts</span></span>
<span data-ttu-id="3c6eb-156">Na de installatie van Hallo OMS-agent voor Linux-pakketten hello volgende aanvullende configuratie van het hele systeem wijzigingen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="3c6eb-157">Deze artefacten zijn verwijderd wanneer Hallo omsagent pakket wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="3c6eb-158">Een onbevoegde gebruiker met de naam: `omsagent` wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="3c6eb-159">Dit is Hallo account Hallo omsagent-daemon wordt uitgevoerd als</span><span class="sxs-lookup"><span data-stu-id="3c6eb-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="3c6eb-160">Een bestand sudoers 'opnemen' gemaakt op /etc/sudoers.d/omsagent dit omsagent toorestart Hallo syslog en omsagent daemons worden geautoriseerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="3c6eb-161">Als sudo "bevatten" richtlijnen worden niet ondersteund in versie van sudo hello geïnstalleerd, wordt deze vermeldingen te/etc/sudoers geschreven.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="3c6eb-162">Hallo syslog-configuratie is gewijzigd tooforward een subset van gebeurtenissen toohello agent.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="3c6eb-163">Zie voor meer informatie, Hallo **gegevensverzameling configureren** onderstaande sectie</span><span class="sxs-lookup"><span data-stu-id="3c6eb-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="3c6eb-164">Linux-Gegevensdetails verzameling</span><span class="sxs-lookup"><span data-stu-id="3c6eb-164">Linux data collection details</span></span>
<span data-ttu-id="3c6eb-165">Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="3c6eb-166">Bron</span><span class="sxs-lookup"><span data-stu-id="3c6eb-166">source</span></span> | <span data-ttu-id="3c6eb-167">Directe Agent</span><span class="sxs-lookup"><span data-stu-id="3c6eb-167">Direct Agent</span></span> | <span data-ttu-id="3c6eb-168">SCOM-agents</span><span class="sxs-lookup"><span data-stu-id="3c6eb-168">SCOM agent</span></span> | <span data-ttu-id="3c6eb-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3c6eb-169">Azure Storage</span></span> | <span data-ttu-id="3c6eb-170">SCOM vereist?</span><span class="sxs-lookup"><span data-stu-id="3c6eb-170">SCOM required?</span></span> | <span data-ttu-id="3c6eb-171">SCOM-agent gegevens die worden verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="3c6eb-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="3c6eb-172">Frequentie van de verzameling</span><span class="sxs-lookup"><span data-stu-id="3c6eb-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3c6eb-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="3c6eb-173">Zabbix</span></span> |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="3c6eb-179">1 minuut</span><span class="sxs-lookup"><span data-stu-id="3c6eb-179">1 minute</span></span> |
| <span data-ttu-id="3c6eb-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="3c6eb-180">Nagios</span></span> |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="3c6eb-186">bij ontvangst</span><span class="sxs-lookup"><span data-stu-id="3c6eb-186">on arrival</span></span> |
| <span data-ttu-id="3c6eb-187">syslog</span><span class="sxs-lookup"><span data-stu-id="3c6eb-187">syslog</span></span> |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="3c6eb-193">naar Azure storage: 10 minuten. Agent: bij ontvangst</span><span class="sxs-lookup"><span data-stu-id="3c6eb-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="3c6eb-194">Linux-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="3c6eb-194">Linux performance counters</span></span> |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="3c6eb-200">Als gepland, minimaal 10 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6eb-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="3c6eb-201">bijhouden van wijzigingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-201">change tracking</span></span> |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="3c6eb-207">elk uur</span><span class="sxs-lookup"><span data-stu-id="3c6eb-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="3c6eb-208">Pakketvereisten</span><span class="sxs-lookup"><span data-stu-id="3c6eb-208">Package Requirements</span></span>
| <span data-ttu-id="3c6eb-209">**Vereist pakket**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-209">**Required package**</span></span> | <span data-ttu-id="3c6eb-210">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-210">**Description**</span></span> | <span data-ttu-id="3c6eb-211">**Minimale versie**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c6eb-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="3c6eb-212">Glibc</span></span> |<span data-ttu-id="3c6eb-213">GNU C-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="3c6eb-213">GNU C library</span></span> |<span data-ttu-id="3c6eb-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="3c6eb-214">2.5-12</span></span> |
| <span data-ttu-id="3c6eb-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="3c6eb-215">Openssl</span></span> |<span data-ttu-id="3c6eb-216">OpenSSL-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-216">OpenSSL libraries</span></span> |<span data-ttu-id="3c6eb-217">0.9.8e of 1.0</span><span class="sxs-lookup"><span data-stu-id="3c6eb-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="3c6eb-218">CURL</span><span class="sxs-lookup"><span data-stu-id="3c6eb-218">Curl</span></span> |<span data-ttu-id="3c6eb-219">WebClient cURL</span><span class="sxs-lookup"><span data-stu-id="3c6eb-219">cURL web client</span></span> |<span data-ttu-id="3c6eb-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="3c6eb-220">7.15.5</span></span> |
| <span data-ttu-id="3c6eb-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="3c6eb-221">Python-ctypes</span></span> |<span data-ttu-id="3c6eb-222">functie-bibliotheken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-222">function libraries</span></span> |<span data-ttu-id="3c6eb-223">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-223">n/a</span></span> |
| <span data-ttu-id="3c6eb-224">PAM</span><span class="sxs-lookup"><span data-stu-id="3c6eb-224">PAM</span></span> |<span data-ttu-id="3c6eb-225">Pluggable authentication Modules</span><span class="sxs-lookup"><span data-stu-id="3c6eb-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="3c6eb-226">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="3c6eb-227">Rsyslog of syslog-ng zijn vereiste toocollect syslog-berichten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="3c6eb-228">Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="3c6eb-229">toocollect syslog-gegevens van deze versie van deze verdelingen Hallo rsyslog daemon moet worden geïnstalleerd en geconfigureerd tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="3c6eb-230">Snelle installatie</span><span class="sxs-lookup"><span data-stu-id="3c6eb-230">Quick install</span></span>
<span data-ttu-id="3c6eb-231">Voer Hallo opdrachten toodownload hello omsagent te volgen, Hallo controlesom, en vervolgens installeren en vrijgeven Hallo agent valideren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="3c6eb-232">Opdrachten zijn voor 64-bits.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-232">Commands are for 64-bit.</span></span> <span data-ttu-id="3c6eb-233">Hallo werkruimte-ID en de primaire sleutel zijn gevonden in Hallo OMS-portal onder **instellingen** op Hallo **verbonden bronnen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![details van de werkruimte](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="3c6eb-235">Er zijn tal van andere methoden tooinstall Hallo agent en een upgrade uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="3c6eb-236">U vindt meer informatie hierover op [stappen tooinstall Hallo OMS-Agent voor Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="3c6eb-237">U kunt ook weergeven Hallo [Azure video-overzicht](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="3c6eb-238">Kies uw Linux gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="3c6eb-239">Hoe u Hallo gegevenstypen die u zou doen zoals toocollect is afhankelijk van of u wilt dat toouse Hallo OMS-portal of als u wilt bewerken, verschillende configuratiebestanden rechtstreeks op uw Linux-clients.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="3c6eb-240">Als u toouse Hallo portal kiest, wordt configuration Hallo tooall van uw Linux-clients automatisch verzonden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="3c6eb-241">Als u verschillende configuraties nodig hebt voor verschillende Linux-clients, wordt u tooedit clientbestanden afzonderlijk – moet of gebruik een alternatief zoals PowerShell DSC, Chef of Puppet.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="3c6eb-242">U kunt opgeven dat Hallo syslog-gebeurtenissen en prestatiemeteritems die u wilt toocollect met behulp van de configuratiebestanden op Hallo Linux-computers.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="3c6eb-243">*Als u gegevensverzameling tooconfigure door agentconfiguratiebestanden te bewerken, moet u de gecentraliseerde configuratie Hallo uitschakelen.*</span><span class="sxs-lookup"><span data-stu-id="3c6eb-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="3c6eb-244">Instructies vindt u hieronder de gegevensverzameling tooconfigure in het Hallo-agent configuratiebestanden, evenals toodisable centrale configuratie voor alle OMS-Agents voor Linux of afzonderlijke computers.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="3c6eb-245">OMS beheer uitschakelt voor een afzonderlijke Linux-computer</span><span class="sxs-lookup"><span data-stu-id="3c6eb-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="3c6eb-246">Gecentraliseerde gegevensverzameling voor configuratiegegevens is uitgeschakeld voor een afzonderlijke Linux-computer met de Hallo OMS_MetaConfigHelper.py script.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="3c6eb-247">Dit is handig als u een subset van de computers moet een specifieke configuratie hebben.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="3c6eb-248">gecentraliseerde configuratie toodisable:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="3c6eb-249">gecentraliseerde configuratie toore inschakelen:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="3c6eb-250">Linux-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="3c6eb-250">Linux performance counters</span></span>
<span data-ttu-id="3c6eb-251">Linux-prestatiemeteritems zijn vergelijkbaar tooWindows prestatiemeteritems: beide op dezelfde manier werkt.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="3c6eb-252">U kunt gebruiken Hallo tooadd procedures te volgen en om ze te configureren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="3c6eb-253">Nadat ze zijn tooOMS toegevoegd, worden gegevens verzameld voor elke 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="3c6eb-254">een Linux-prestatiemeteritem in OMS tooadd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="3c6eb-255">tooconfigure OMS-Agents voor Linux met Hallo OMS-portal, kunt u Linux-prestatiemeteritems toevoegen op de pagina instellingen Hallo op **gegevens**.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="3c6eb-256">Op Hallo **instellingen** pagina onder **gegevens** , klikt u op **Linux prestatiemeteritems** en vervolgens selecteren of typen naam Hallo Hallo-item dat u wilt dat tooadd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="3c6eb-257">![gegevens](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="3c6eb-258">Als u de volledige naam van de teller Hallo Hallo niet weet, kunt u een gedeeltelijke naam te typen starten en een lijst met beschikbare items weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="3c6eb-259">Wanneer u Hallo teller vindt u tooadd wilt, klikt u op naam in de lijst Hallo Hallo en klik vervolgens op Hallo plus pictogram tooadd Hallo teller.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="3c6eb-260">Nadat u Hallo teller toevoegt, wordt deze weergegeven in Hallo lijst met items die zijn gemarkeerd met een gekleurde balk.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="3c6eb-261">Standaard Hallo **toepassen onderstaande configuratie toomy computers** optie is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="3c6eb-262">Als u verzenden van configuratiegegevens toodisable wilt, schakelt u Hallo selectie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="3c6eb-263">Wanneer u klaar bent wijzigen prestatiemeteritems Hallo Hallo pagina onderaan in klikt u op **opslaan** toofinalize uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="3c6eb-264">Hallo-configuratiewijzigingen die u hebt aangebracht worden vervolgens tooall Hallo OMS Agents verzonden voor Linux die zijn geregistreerd bij OMS, meestal binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="3c6eb-265">Linux-prestatiemeteritems in OMS configureren</span><span class="sxs-lookup"><span data-stu-id="3c6eb-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="3c6eb-266">Voor Windows-prestatiemeteritems kunt u een specifiek exemplaar voor elk prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="3c6eb-267">Voor Linux-prestatiemeteritems, echter geldt elk exemplaar van een prestatiemeteritem die u kiest tooall onderliggende items van Hallo bovenliggende item.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="3c6eb-268">Hallo volgende tabel bevat algemene Hallo-exemplaren beschikbaar tooboth Linux- en Windows-prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="3c6eb-269">**Exemplaarnaam**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-269">**Instance name**</span></span> | <span data-ttu-id="3c6eb-270">**Betekenis**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="3c6eb-271">\_Totaal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-271">\_Total</span></span> |<span data-ttu-id="3c6eb-272">Totaal van alle exemplaren van Hallo</span><span class="sxs-lookup"><span data-stu-id="3c6eb-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="3c6eb-273">Alle exemplaren</span><span class="sxs-lookup"><span data-stu-id="3c6eb-273">All instances</span></span> |
| <span data-ttu-id="3c6eb-274">(/ &#124; / var)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-274">(/&#124;/var)</span></span> |<span data-ttu-id="3c6eb-275">Komt overeen met de exemplaren met de naam: / of /var</span><span class="sxs-lookup"><span data-stu-id="3c6eb-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="3c6eb-276">Op dezelfde manier geldt Hallo controle-interval die u kiest voor een bovenliggend item tooall de onderliggende items.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="3c6eb-277">Met andere woorden, zijn alle onderliggende item controle-intervallen Hallo en exemplaren onderling verbonden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="3c6eb-278">Toevoegen en maatstaven voor prestaties configureren met Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="3c6eb-279">Prestaties metrische gegevens toocollect worden beheerd door Hallo configuratie in/etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="3c6eb-280">Zie [maatstaven voor prestaties beschikbaar](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) voor beschikbare klassen en metrische gegevens voor Hallo OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="3c6eb-281">Elk object of de categorie van prestaties metrische gegevens toocollect moet worden gedefinieerd in het configuratiebestand Hallo als één `<source>` element.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="3c6eb-282">Hallo syntaxis volgt Hallo patroon hieronder.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="3c6eb-283">Hallo configureerbare parameters van dit element zijn:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="3c6eb-284">**Object\_naam**: Hallo objectnaam voor Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="3c6eb-285">**Exemplaar\_regex**: een *reguliere expressie* definiëren welke toocollect exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="3c6eb-286">Hallo waarde: `.*` bevat alle exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="3c6eb-287">toocollect processor metrische gegevens voor alleen Hallo \_totaalwaarde, kunt u opgeven `_Total`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="3c6eb-288">Procesgegevens toocollect voor hello alleen crond of sshd exemplaren, kunt u opgeven: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="3c6eb-289">**Teller\_naam\_regex**: een *reguliere expressie* definiëren welke toocollect tellers (voor Hallo object).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="3c6eb-290">toocollect alle meteritems voor het Hallo-object opgeven: `.*`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="3c6eb-291">toocollect wisselen alleen ruimte tellers voor Hallo geheugenobject, die u kunt opgeven:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="3c6eb-292">**Interval:**: Hallo frequentie op welke Hallo van het object prestatiemeteritems worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="3c6eb-293">Hallo standaardconfiguratie voor maatstaven voor prestaties is:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-293">hello default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="3c6eb-294">MySQL-prestatiemeteritems met Linux-opdrachten inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="3c6eb-295">Als MySQL-Server of MariaDB Server wordt gedetecteerd op de computer Hallo wanneer Hallo omsagent bundel is geïnstalleerd, wordt automatisch een prestatiebewaking-provider voor de MySQL-Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="3c6eb-296">Deze provider verbindt toohello lokale MySQL/MariaDB server tooexpose prestatiestatistieken weer.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="3c6eb-297">U moet tooconfigure MySQL gebruikersreferenties zodat hello provider toegang heeft tot Hallo MySQL-Server.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="3c6eb-298">toodefine een standaardgebruiker rekening gehouden met Hallo MySQL-server op localhost, gebruik Hallo opdracht voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="3c6eb-299">Hallo referentiebestand moet worden gelezen door Hallo omsagent account.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="3c6eb-300">Hallo mycimprovauth opdracht uitgevoerd als omsgent wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="3c6eb-301">U kunt ook opgeven Hallo MySQL-referenties in een bestand vereist door Hallo-bestand te maken: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Zie voor meer informatie over het beheren van MySQL-referenties voor de bewaking via Hallo mysql-auth bestand [beheren MySQL bewaking van de referenties in Hallo verificatiebestand](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="3c6eb-302">Zie [machtigingen die vereist zijn voor de prestatiemeteritems MySQL-Database](#database-permissions-required-for-mysql-performance-counters) voor meer informatie over de machtigingen vereist voor Hallo MySQL gebruiker toocollect prestatiegegevens MySQL-Server.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="3c6eb-303">Apache HTTP-Server-prestatiemeteritems met Linux-opdrachten inschakelen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="3c6eb-304">Als de Apache HTTP-Server op Hallo-computer wordt gedetecteerd wanneer Hallo omsagent bundel is geïnstalleerd, wordt automatisch een prestatiebewaking-provider voor de Apache HTTP-Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="3c6eb-305">Deze provider is afhankelijk van een Apache 'module', die moet worden geladen in Hallo Apache HTTP-Server in de volgorde tooaccess prestatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="3c6eb-306">U kunt Hallo-module laden Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="3c6eb-307">toounload hello Apache bewakingsmodule, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="3c6eb-308">de prestatiegegevens tooview met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="3c6eb-309">Klik op Hallo logboek zoeken tegel in Hallo Operations Management Suite-portal.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="3c6eb-310">Typ in de zoekbalk hello, `* (Type=Perf)` tooview alle prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="3c6eb-311">Omdat OMS ook Windows-prestatiemeteritemgegevens verzamelt, u moet bereik omlaag Hallo zoeken tooLinux-specifieke gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="3c6eb-312">Dus hello volgende voorbeeld zou show prestaties gegevens specifieke tooan voorbeeld Linux-server met de naam Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![Voorbeeld van de server weergegeven in zoekresultaten](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="3c6eb-314">In het Hallo-resultaten, kunt u **metrische gegevens** tooview Hallo tellers die de gegevens zijn verzameld voor.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="3c6eb-315">Realtime-gegevens wordt weergegeven als grafieken voor elk prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-315">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="3c6eb-317">Syslog</span><span class="sxs-lookup"><span data-stu-id="3c6eb-317">Syslog</span></span>
<span data-ttu-id="3c6eb-318">Syslog is een protocol vergelijkbare tooWindows gebeurtenislogboeken voor logboekregistratie: beide op dezelfde manier werken wanneer weergegeven in OMS.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="3c6eb-319">een nieuwe Linux syslog-faciliteit in OMS tooadd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="3c6eb-320">Op Hallo **instellingen** pagina onder **gegevens** , klikt u op **Syslog** en toohello links Hallo plus pictogram, typ Hallo-naam van Hallo syslog-faciliteit die u tooadd wilt.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="3c6eb-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="3c6eb-322">Als u de volledige naam van de faciliteit Hallo Hallo niet weet, kunt u starten een gedeeltelijke naam te typen en een lijst met beschikbare syslog faciliteiten wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="3c6eb-323">Als u merkt dat Hallo syslog-faciliteit dat u tooadd wilt, klikt u op de naam Hallo in Hallo lijst en klik vervolgens op Hallo plus pictogram tooadd Hallo syslog-faciliteit.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="3c6eb-324">Nadat u hebt toegevoegd Hallo faciliteit, wordt deze weergegeven in de lijst met Hallo gemarkeerd met een gekleurde balk.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="3c6eb-325">Kies vervolgens Hallo ernstcategorieën (gegevenscategorieën syslog-faciliteit) dat u wilt dat toocollect.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="3c6eb-326">Klik onderaan Hallo Hallo pagina **opslaan** toofinalize uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="3c6eb-327">Hallo-configuratiewijzigingen die u hebt aangebracht worden vervolgens tooall Hallo OMS Agents verzonden voor Linux die zijn geregistreerd bij OMS, meestal binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="3c6eb-328">Configureren van Linux syslog faciliteiten in Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="3c6eb-329">Syslog-gebeurtenissen van Hallo syslog-daemon worden verzonden, bijvoorbeeld rsyslog of syslog-ng, tooa lokale poort die Hallo-agent luistert op.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="3c6eb-330">Standaard poort 25224.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-330">By default, port 25224.</span></span> <span data-ttu-id="3c6eb-331">Wanneer het Hallo-agent is geïnstalleerd, wordt een standaardconfiguratie syslog toegepast.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="3c6eb-332">U vindt deze op:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-332">This is found at:</span></span>

<span data-ttu-id="3c6eb-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="3c6eb-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="3c6eb-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="3c6eb-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="3c6eb-335">Hallo OMS-agent syslog standaardconfiguratie bestandsuploads syslog-gebeurtenissen van alle installaties met een ernst van waarschuwing of hoger.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="3c6eb-336">Als u syslog-configuratie Hallo bewerkt, moet u Hallo syslog-daemon voor Hallo wijzigingen tootake effect opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="3c6eb-337">Hallo syslog standaardconfiguratie voor Hallo OMS-Agent voor Linux voor OMS is:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="3c6eb-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="3c6eb-338">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="3c6eb-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="3c6eb-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="3c6eb-340">tooview alle Syslog-gebeurtenissen met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="3c6eb-341">Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="3c6eb-342">In Hallo **Log-beheer** groeperen, kies een vooraf gedefinieerde syslog-zoekopdracht en selecteer vervolgens een toorun deze.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="3c6eb-343">Dit voorbeeld toont alle Syslog-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-343">This example shows all Syslog events.</span></span>

![Syslog-gebeurtenissen wordt weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="3c6eb-345">U kunt nu inzoomen in zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="3c6eb-346">Linux-waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-346">Linux alerts</span></span>
<span data-ttu-id="3c6eb-347">Als u Nagios of Zabbix toomanage die uw Linux-machines en klik vervolgens op OMS Hallo waarschuwingen gegenereerd op basis van deze hulpprogramma's kunt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="3c6eb-348">Er is echter momenteel geen methode tooconfigure binnenkomende waarschuwingsgegevens met Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="3c6eb-349">In plaats daarvan moet u een configuratie-bestand toostart verzenden waarschuwingen tooOMS tooedit.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="3c6eb-350">Waarschuwingen verzamelen van Nagios</span><span class="sxs-lookup"><span data-stu-id="3c6eb-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="3c6eb-351">toocollect waarschuwingen van een Nagios-server, moet u toomake Hallo configuratiewijzigingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="3c6eb-352">Verleen Hallo gebruiker **omsagent** leestoegang toohello Nagios-logboekbestand (dat wil zeggen /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="3c6eb-353">Ervan uitgaande dat Hallo nagios.log bestand eigendom is van de groep Hallo **nagios** , kunt u Hallo gebruiker toevoegen **omsagent** toohello **nagios** groep.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="3c6eb-354">Hallo omsagent.confconfiguration bestand wijzigen (/ etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="3c6eb-355">Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="3c6eb-356">Opnieuw opstarten Hallo omsagent daemon:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="3c6eb-357">Waarschuwingen verzamelen van Zabbix</span><span class="sxs-lookup"><span data-stu-id="3c6eb-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="3c6eb-358">toocollect waarschuwingen van een server Zabbix u zult vergelijkbare stappen toothose uitvoeren voor Nagios hierboven, maar u moet een gebruiker toospecify en het wachtwoord in *leesbare tekst*.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="3c6eb-359">Dit is niet ideaal, maar zullen waarschijnlijk snel veranderen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="3c6eb-360">tooaddress dit probleem, raden we aan dat u Hallo gebruiker en het alleen toomonitor toestemming geven.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="3c6eb-361">Een voorbeeld in deze sectie van Hallo omsagent.conf-configuratiebestand (/ etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf) voor Zabbix moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="3c6eb-362">Waarschuwingen weergeven in de zoekopdracht Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="3c6eb-363">Nadat u uw Linux-computers toosend waarschuwingen tooOMS hebt geconfigureerd, kunt u een paar eenvoudige logboek query's tooview Hallo waarschuwingen voor zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="3c6eb-364">Hallo retourneert volgende search query voorbeeld alle Hallo vastgelegd waarschuwingen die zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="3c6eb-365">Bijvoorbeeld, als bepaald soort probleem in uw IT-infrastructuur optreedt, resultaten vervolgens voor Hallo volgt query kan erop wijzen waar Hallo probleem mogelijk afkomstig zijn.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="3c6eb-366">En u kunt eenvoudig inzoomen in toohello waarschuwingen door bron system toohelp smalle uw onderzoek.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="3c6eb-367">Hallo voordeel is dat u niet per se toogo toovarious beheersystemen van Hallo begin hebt, mits uw waarschuwingen worden verzonden tooOMS, u er kunt starten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="3c6eb-368">tooview alle Nagios waarschuwingen met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="3c6eb-369">Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="3c6eb-370">Typ in Hallo query-balk Hallo volgende zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="3c6eb-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios waarschuwingen weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="3c6eb-372">Nadat u de zoekresultaten Hallo ziet, u kunt inzoomen op aanvullende informatie zoals *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="3c6eb-373">tooview alle Zabbix waarschuwingen met Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="3c6eb-374">Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="3c6eb-375">Typ in Hallo query-balk Hallo volgende zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="3c6eb-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix waarschuwingen weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="3c6eb-377">Nadat u de zoekresultaten Hallo ziet, u kunt inzoomen op aanvullende informatie zoals *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="3c6eb-378">Compatibiliteit met System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3c6eb-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="3c6eb-379">Hallo OMS-Agent voor Linux deelt agent binaire bestanden met Hallo System Center Operations Manager-agent.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="3c6eb-380">Hallo OMS-Agent voor Linux installeren op een systeem dat momenteel wordt beheerd door Operations Manager-upgrades Hallo OMI en SCX-pakketten op Hallo computer tooa nieuwere versie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="3c6eb-381">Hallo OMS-Agent voor Linux en System Center 2012 R2 zijn compatibel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="3c6eb-382">Echter **System Center 2012 SP1 en eerdere versies zijn momenteel niet compatibel of ondersteund Hello OMS-Agent voor Linux.**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="3c6eb-383">Als Hallo OMS-Agent voor Linux is geïnstalleerd tooa-computer die momenteel niet wordt beheerd door Operations Manager en u wilt dat later toomanage Hallo computer met Operations Manager, moet u Hallo OMI-configuratie wijzigen voordat u Hallo-computer detecteren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="3c6eb-384">**Deze stap is niet nodig als Hallo Operations Manager-agent is geïnstalleerd voordat Hallo OMS-Agent voor Linux.**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="3c6eb-385">tooenable hello OMS-Agent voor Linux-toocommunicate met Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3c6eb-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="3c6eb-386">Hallo bestand /etc/opt/omi/conf/omiserver.conf bewerken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="3c6eb-387">Zorg ervoor dat Hallo regels die beginnen met **httpsport =** Hallo poort 1270 definieert.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="3c6eb-388">Zoals`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="3c6eb-389">Opnieuw opstarten Hallo OMI-server:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="3c6eb-390">Databasemachtigingen vereist voor de MySQL-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="3c6eb-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="3c6eb-391">toogrant machtigingen tooa MySQL bewaking van gebruiker, Hallo verlenen gebruiker hebben de bevoegdheid 'GRANT optie' hello, evenals Hallo bevoegdheid wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="3c6eb-392">Opdat Hallo MySQL gebruiker tooreturn prestaties gegevens Hallo gebruiker wordt moet toegang tot toohello query's te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="3c6eb-393">Bovendien toothese query's Hallo MySQL is vereist, selecteer toegang toohello standaardtabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="3c6eb-394">INFORMATION_SCHEMA</span><span class="sxs-lookup"><span data-stu-id="3c6eb-394">information_schema</span></span>
* <span data-ttu-id="3c6eb-395">MySQL</span><span class="sxs-lookup"><span data-stu-id="3c6eb-395">mysql</span></span>

<span data-ttu-id="3c6eb-396">Deze rechten kunnen worden verleend door het uitvoeren van Hallo grant opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="3c6eb-397">MySQL-referenties in Hallo verificatiebestand bewaking beheren</span><span class="sxs-lookup"><span data-stu-id="3c6eb-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="3c6eb-398">Hallo volgende secties u MySQL referenties beheren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="3c6eb-399">Hallo MySQL OMI provider configureren</span><span class="sxs-lookup"><span data-stu-id="3c6eb-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="3c6eb-400">Hallo MySQL OMI provider moet de gebruiker vooraf geconfigureerde MySQL en MySQL-clientbibliotheken geïnstalleerd in tooquery Hallo prestatiestatus/ordergegevens van Hallo MySQL-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="3c6eb-401">MySQL OMI verificatiebestand</span><span class="sxs-lookup"><span data-stu-id="3c6eb-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="3c6eb-402">MySQL OMI-provider gebruikt een verificatie-bestand toodetermine welk exemplaar bind-adres en poort Hallo MySQL luistert en wat referenties toouse toogather metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="3c6eb-403">Tijdens de installatie Hallo MySQL OMI scant provider MySQL my.cnf configuratiebestanden (standaardlocaties) voor bind-adres en poort en gedeeltelijk set Hallo verificatiebestand MySQL OMI.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="3c6eb-404">toocomplete bewaking van een MySQL-server-exemplaar, een bestand voor verificatie van vooraf gegenereerde MySQL OMI toevoegen in de juiste map Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="3c6eb-405">Verificatie-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="3c6eb-405">Authentication file format</span></span>
<span data-ttu-id="3c6eb-406">Hallo verificatiebestand MySQL OMI is een tekstbestand dat informatie bevat over:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="3c6eb-407">Poort</span><span class="sxs-lookup"><span data-stu-id="3c6eb-407">Port</span></span>
* <span data-ttu-id="3c6eb-408">BIND-adres</span><span class="sxs-lookup"><span data-stu-id="3c6eb-408">Bind-Address</span></span>
* <span data-ttu-id="3c6eb-409">MySQL-gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="3c6eb-409">MySQL username</span></span>
* <span data-ttu-id="3c6eb-410">Base64-gecodeerd wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3c6eb-410">Base64 encoded password</span></span>

<span data-ttu-id="3c6eb-411">Hallo MySQL OMI verificatiebestand verleent alleen machtigingen voor lezen/schrijven toohello Linux gebruiker die wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="3c6eb-412">Een standaard MySQL OMI verificatiebestand bevat een standaardexemplaar en een poortnummer, afhankelijk van welke informatie beschikbaar is en geparseerde van Hallo MySQL-configuratiebestand is gevonden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="3c6eb-413">Hallo-standaardexemplaar is een manier toomake meerdere MySQL-exemplaren op een Linux-host eenvoudiger beheren en wordt aangegeven door de instantie Hallo met poort 0.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="3c6eb-414">Eigenschappen instellen van het standaardexemplaar Hallo worden overgenomen door alle toegevoegde exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="3c6eb-415">Bijvoorbeeld als MySQL exemplaar luisteren op poort '3308' wordt toegevoegd, Hallo standaardexemplaar bind-adres, gebruikersnaam en wachtwoord Base64-gecodeerd wordt gebruikte tootry worden en Hallo exemplaar luistert op 3308 bewaken.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="3c6eb-416">Hallo-exemplaar op 3308 is verbonden tooanother adres en gebruikt Hallo dezelfde MySQL-gebruikersnaam en wachtwoord paar alleen respecification Hallo Hallo bind-adres is vereist als hello andere eigenschappen worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="3c6eb-417">Voorbeelden van Hallo verificatiebestand lijken op Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="3c6eb-418">Standaard-instantie en -exemplaar met poort 3308:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="3c6eb-419">Standaard-instantie en -exemplaar met poort 3308 + verschillende Base 64 gecodeerde wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="3c6eb-420">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-420">**Property**</span></span> | <span data-ttu-id="3c6eb-421">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3c6eb-422">Poort</span><span class="sxs-lookup"><span data-stu-id="3c6eb-422">Port</span></span> |<span data-ttu-id="3c6eb-423">Poort vertegenwoordigt Hallo huidige poort Hallo MySQL exemplaar luistert op.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="3c6eb-424">Hallo poort 0 betekent dat na Hallo-eigenschappen worden gebruikt voor het standaardexemplaar.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="3c6eb-425">BIND-adres</span><span class="sxs-lookup"><span data-stu-id="3c6eb-425">Bind-Address</span></span> |<span data-ttu-id="3c6eb-426">Hallo adres binden is Hallo huidige MySQL bind-adres</span><span class="sxs-lookup"><span data-stu-id="3c6eb-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="3c6eb-427">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="3c6eb-427">username</span></span> |<span data-ttu-id="3c6eb-428">Deze gebruikersnaam Hallo van Hallo MySQL gebruiker gewenste toouse toomonitor Hallo MySQL server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="3c6eb-429">Base64-gecodeerd wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3c6eb-429">Base64 encoded Password</span></span> |<span data-ttu-id="3c6eb-430">Dit is een wachtwoord op Hallo van Hallo MySQL bewaking gebruiker gecodeerd in Base64.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="3c6eb-431">Automatisch bijwerken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-431">AutoUpdate</span></span> |<span data-ttu-id="3c6eb-432">Hallo MySQL OMI Provider is bijgewerkt wordt Hallo-provider opnieuw scannen op wijzigingen in Hallo my.cnf bestand als Hallo MySQL OMI verificatie bestand overschrijven.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="3c6eb-433">Deze vlag tootrue of ONWAAR, afhankelijk van de vereiste updates toohello MySQL OMI verificatiebestand ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="3c6eb-434">Bestandslocatie van verificatie</span><span class="sxs-lookup"><span data-stu-id="3c6eb-434">Authentication file location</span></span>
<span data-ttu-id="3c6eb-435">Hallo MySQL OMI verificatiebestand moet Hallo volgende locatie plaatsen en met de naam 'mysql-auth':</span><span class="sxs-lookup"><span data-stu-id="3c6eb-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="3c6eb-436">/var/opt/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth</span><span class="sxs-lookup"><span data-stu-id="3c6eb-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="3c6eb-437">Hallo-bestand (en auth/omsagent directory) dient het eigendom van Hallo omsagent gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="3c6eb-438">Agent-logboeken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-438">Agent logs</span></span>
<span data-ttu-id="3c6eb-439">Hallo-logboeken voor Hallo OMS-Agent voor Linux bevindt zich in:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="3c6eb-440">/ var/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="3c6eb-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="3c6eb-441">Hallo-logboeken voor Hallo OMS-Agent voor Linux voor omsconfig (agentconfiguratie) programma bevindt zich in:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="3c6eb-442">/ var/opt/microsoft/omsconfig/log /</span><span class="sxs-lookup"><span data-stu-id="3c6eb-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="3c6eb-443">Logboeken voor Hallo OMI en SCX-onderdelen (die prestatiegegevens van de metrische gegevens bieden) bevindt zich in:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="3c6eb-444">/ var/opt/omi/log/en /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="3c6eb-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="3c6eb-445">Hallo OMS-Agent voor probleemoplossing voor Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="3c6eb-446">Gebruik Hallo informatie toodiagnose te volgen en oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="3c6eb-447">Als geen Hallo probleemoplossingsinformatie in deze sectie u helpt, kunt u ook gebruiken Hallo na resources toohelp los het probleem.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="3c6eb-448">Klanten met Premier support kan zich aanmelden een ondersteuningsaanvraag via [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="3c6eb-449">Klanten met Azure support-overeenkomsten kunnen aanmelden ondersteuningsaanvragen Hallo [Azure-portal](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="3c6eb-450">Bestand een [GitHub probleem](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="3c6eb-451">Feedbackforum voor ideeën en toocreate een foutenrapport [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="3c6eb-452">Belangrijke logboeklocaties</span><span class="sxs-lookup"><span data-stu-id="3c6eb-452">Important log locations</span></span>
| <span data-ttu-id="3c6eb-453">File</span><span class="sxs-lookup"><span data-stu-id="3c6eb-453">File</span></span> | <span data-ttu-id="3c6eb-454">Pad</span><span class="sxs-lookup"><span data-stu-id="3c6eb-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="3c6eb-455">OMS-Agent voor Linux-logboekbestand</span><span class="sxs-lookup"><span data-stu-id="3c6eb-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="3c6eb-456">Configuratielogboekbestand voor OMS-Agent</span><span class="sxs-lookup"><span data-stu-id="3c6eb-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="3c6eb-457">Belangrijke configuratie-bestanden</span><span class="sxs-lookup"><span data-stu-id="3c6eb-457">Important configuration files</span></span>
| <span data-ttu-id="3c6eb-458">Catergory</span><span class="sxs-lookup"><span data-stu-id="3c6eb-458">Catergory</span></span> | <span data-ttu-id="3c6eb-459">Bestandslocatie</span><span class="sxs-lookup"><span data-stu-id="3c6eb-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="3c6eb-460">Syslog</span><span class="sxs-lookup"><span data-stu-id="3c6eb-460">Syslog</span></span> |<span data-ttu-id="3c6eb-461">`/etc/syslog-ng/syslog-ng.conf`of `/etc/rsyslog.conf` of`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="3c6eb-462">Prestaties, Nagios, Zabbix, OMS-uitvoer en algemene agent</span><span class="sxs-lookup"><span data-stu-id="3c6eb-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="3c6eb-463">Aanvullende configuraties</span><span class="sxs-lookup"><span data-stu-id="3c6eb-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="3c6eb-464">Bewerking configuratiebestanden voor prestatiemeteritems en syslog overschreven als de configuratie van de OMS-Portal is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="3c6eb-465">U kunt de configuratie in Hallo OMS-Portal (voor alle knooppunten) uitschakelen of voor afzonderlijke knooppunten door het uitvoeren van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="3c6eb-466">Inschakelen van logboekregistratie voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="3c6eb-466">Enable debug logging</span></span>
<span data-ttu-id="3c6eb-467">tooenable foutopsporing aan te melden, kunt u Hallo OMS uitvoer-invoegtoepassing en de uitgebreide uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="3c6eb-468">OMS-invoegtoepassing voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="3c6eb-468">OMS output plugin</span></span>
<span data-ttu-id="3c6eb-469">FluentD kunt Hallo invoegtoepassing toospecify niveaus voor logboekregistratie voor verschillende logboekniveaus voor invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="3c6eb-470">een ander logboek-niveau voor OMS-uitvoer toospecify Hallo algemeen agentconfiguratie in Hallo bewerken `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` bestand.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="3c6eb-471">Wijzigen in de buurt Hallo onderkant van het configuratiebestand Hallo Hallo `log_level` eigenschap uit `info` te`debug`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="3c6eb-472">Logboekregistratie voor foutopsporing kunt u toosee batch verwerkt uploads toohello OMS-Service door type, het aantal gegevensitems en toosend tijd gescheiden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="3c6eb-473">*Voorbeeld van het logboek voor foutopsporing is ingeschakeld:*</span><span class="sxs-lookup"><span data-stu-id="3c6eb-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="3c6eb-474">Uitgebreide uitvoer</span><span class="sxs-lookup"><span data-stu-id="3c6eb-474">Verbose output</span></span>
<span data-ttu-id="3c6eb-475">In plaats van Hallo OMS uitvoer-invoegtoepassing, kunt u ook uitvoeren gegevensitems rechtstreeks te`stdout`, die wordt weergegeven in Hallo OMS-Agent voor Linux-logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="3c6eb-476">In het Hallo OMS algemeen agent-configuratiebestand op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commentarieer Hallo OMS uitvoer invoegtoepassing door toe te voegen een `#` voor elke regel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="3c6eb-477">Hieronder Hallo uitvoer-invoegtoepassing, Hallo Opmerking verwijderen in de volgende sectie door het verwijderen van Hallo Hallo `#` symbool op Hallo begin van elke regel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="3c6eb-478">Doorgestuurde Syslog-berichten worden niet weergegeven in het Hallo-logboek</span><span class="sxs-lookup"><span data-stu-id="3c6eb-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-479">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-479">Probable causes</span></span>
* <span data-ttu-id="3c6eb-480">Hallo toegepast toohello Linux configuratieserver niet verzamelen van Hallo verzonden faciliteiten toestaan en/of meld niveaus</span><span class="sxs-lookup"><span data-stu-id="3c6eb-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="3c6eb-481">Syslog is niet doorgestuurd correct toohello Linux-server</span><span class="sxs-lookup"><span data-stu-id="3c6eb-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="3c6eb-482">Hallo aantal berichten per seconde wordt doorgestuurd zijn te groot voor de basisconfiguratie Hallo Hallo OMS-Agent voor Linux toohandle</span><span class="sxs-lookup"><span data-stu-id="3c6eb-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-483">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-483">Resolutions</span></span>
* <span data-ttu-id="3c6eb-484">Verifieer dat Hallo-configuratie in Hallo OMS-Portal voor Syslog alle Hallo opslagruimten en de juiste logboekniveaus Hallo heeft</span><span class="sxs-lookup"><span data-stu-id="3c6eb-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="3c6eb-485">**OMS-Portal > Instellingen > gegevens > Syslog**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="3c6eb-486">Controleren of deze systeemeigen syslog daemons messaging (`rsyslog`, `syslog-ng`) kunnen tooreceive worden doorgestuurd Hallo-berichten</span><span class="sxs-lookup"><span data-stu-id="3c6eb-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="3c6eb-487">Controleer de instellingen van de firewall op Hallo Syslog-server tooensure dat berichten worden niet geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="3c6eb-488">Een Syslog-bericht tooOMS met Hallo simuleren `logger` command - voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="3c6eb-489">TooOMS voor netwerkverbindingsproblemen als u een proxy</span><span class="sxs-lookup"><span data-stu-id="3c6eb-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-490">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-490">Probable causes</span></span>
* <span data-ttu-id="3c6eb-491">Hallo proxy opgegeven wanneer het Hallo-agent installeren en configureren onjuist</span><span class="sxs-lookup"><span data-stu-id="3c6eb-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="3c6eb-492">Hallo OMS-Service-eindpunten zijn niet whitelistested in uw datacenter</span><span class="sxs-lookup"><span data-stu-id="3c6eb-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-493">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-493">Resolutions</span></span>
* <span data-ttu-id="3c6eb-494">Hallo OMS-Agent installeren met behulp van de volgende opdracht met de optie Hallo Hallo Linux `-v` ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="3c6eb-495">Hiermee worden uitgebreide uitvoer van Hallo agent een verbinding via Hallo proxy toohello OMS-Service.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="3c6eb-496">Hallo-documentatie voor OMS-proxy op lezen [Hallo-agent configureren voor gebruik met een HTTP-proxyserver](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="3c6eb-497">Controleer of deze Hallo OMS-Service-eindpunten te volgen zijn goedgekeurde lijst</span><span class="sxs-lookup"><span data-stu-id="3c6eb-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="3c6eb-498">Agentresource</span><span class="sxs-lookup"><span data-stu-id="3c6eb-498">Agent Resource</span></span> | <span data-ttu-id="3c6eb-499">Poorten</span><span class="sxs-lookup"><span data-stu-id="3c6eb-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="3c6eb-500">&#42;. ods.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="3c6eb-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="3c6eb-501">Poort 443</span><span class="sxs-lookup"><span data-stu-id="3c6eb-501">Port 443</span></span> |
| <span data-ttu-id="3c6eb-502">&#42;. OMS.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="3c6eb-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="3c6eb-503">Poort 443</span><span class="sxs-lookup"><span data-stu-id="3c6eb-503">Port 443</span></span> |
| <span data-ttu-id="3c6eb-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="3c6eb-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="3c6eb-505">Poort 443</span><span class="sxs-lookup"><span data-stu-id="3c6eb-505">Port 443</span></span> |
| <span data-ttu-id="3c6eb-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="3c6eb-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="3c6eb-507">Poort 443</span><span class="sxs-lookup"><span data-stu-id="3c6eb-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="3c6eb-508">Een fout 403 wordt weergegeven wanneer het voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3c6eb-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-509">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-509">Probable causes</span></span>
* <span data-ttu-id="3c6eb-510">Hallo-datum en tijd zijn onjuist op Linux-Server</span><span class="sxs-lookup"><span data-stu-id="3c6eb-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="3c6eb-511">Hallo werkruimte-ID en Werkruimtesleutel gebruikt, zijn onjuist</span><span class="sxs-lookup"><span data-stu-id="3c6eb-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="3c6eb-512">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3c6eb-512">Resolution</span></span>
* <span data-ttu-id="3c6eb-513">Hallo tijd op uw Linux-server met Hallo controleren `date` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="3c6eb-514">Als Hallo gegevens groter dan is of kleiner zijn dan 15 minuten van hello huidige tijd, mislukt de voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="3c6eb-515">toocorrect dit Hallo datum en/of de tijdzone van uw Linux-server bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="3c6eb-516">meest recente versie van de Hallo Hallo OMS-Agent voor Linux een melding als een tijdverschil is ontstaan in voorbereiding</span><span class="sxs-lookup"><span data-stu-id="3c6eb-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="3c6eb-517">Met behulp van RE vrijgeven Hallo juiste werkruimte-ID en Werkruimtesleutel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="3c6eb-518">Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="3c6eb-519">Een 500 fout of 404-fout weergegeven in het logboekbestand Hallo na het voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3c6eb-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="3c6eb-520">Dit is een bekend probleem dat tijdens het Hallo eerste uploaden van gegevens van Linux in een OMS-werkruimte optreedt.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="3c6eb-521">Dit geldt niet voor gegevens die worden verzonden of andere problemen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="3c6eb-522">U kunt negeren Hallo fouten bij het in eerste instantie voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="3c6eb-523">Nagios-gegevens worden niet weergegeven in Hallo OMS-Portal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-524">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-524">Probable causes</span></span>
* <span data-ttu-id="3c6eb-525">Hallo omsagent gebruiker heeft geen machtigingen tooread uit Hallo Nagios-logboekbestand</span><span class="sxs-lookup"><span data-stu-id="3c6eb-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="3c6eb-526">Hello Nagios-bron- en filter secties zijn nog steeds toegelicht in Hallo omsagent.conf bestand</span><span class="sxs-lookup"><span data-stu-id="3c6eb-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-527">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-527">Resolutions</span></span>
* <span data-ttu-id="3c6eb-528">Hallo omsagent gebruiker toevoegen in de volgorde tooread uit Hallo Nagios-bestand.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="3c6eb-529">Zie [Nagios waarschuwingen](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="3c6eb-530">Hallo in OMS-Agent voor Linux-algemeen configuratiebestand op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, zorg ervoor dat **beide** Hallo Nagios bron- en filter secties verwijderd hebt, opmerkingen vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="3c6eb-531">Linux-gegevens worden niet weergegeven in Hallo OMS-Portal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-532">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-532">Probable causes</span></span>
* <span data-ttu-id="3c6eb-533">Onboarding toohello OMS-Service is mislukt</span><span class="sxs-lookup"><span data-stu-id="3c6eb-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="3c6eb-534">Verbinding toohello OMS-Service is geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="3c6eb-535">Hallo OMS-Agent voor Linux-gegevens is een back-up</span><span class="sxs-lookup"><span data-stu-id="3c6eb-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-536">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-536">Resolutions</span></span>
* <span data-ttu-id="3c6eb-537">Controleren dat onboarding toohello OMS-Service is gelukt door te controleren die Hallo `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="3c6eb-538">Met behulp van RE vrijgeven Hallo omsadmin.sh vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="3c6eb-539">Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="3c6eb-540">Als een proxy, gebruikt u Hallo proxy stappen hierboven</span><span class="sxs-lookup"><span data-stu-id="3c6eb-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="3c6eb-541">Wanneer Hallo OMS-Agent voor Linux kan niet met de Hallo OMS-Service communiceren is gegevens op Hallo Agent in sommige gevallen een back-up toohello volledige buffergrootte van 50 MB.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="3c6eb-542">Start Hallo OMS-Agent opnieuw voor Linux met Hallo `/opt/microsoft/omsagent/bin/service_control restart` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="3c6eb-543">Dit probleem is opgelost in Agent versie 1.1.0-28 en hoger.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="3c6eb-544">Syslog Linux prestaties teller configuratie niet wordt toegepast op Hallo OMS-portal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-545">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-545">Probable causes</span></span>
* <span data-ttu-id="3c6eb-546">Hallo configuration-agent in Hallo OMS-Agent voor Linux heeft niet de meest recente configuratie Hallo opgehaald uit Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="3c6eb-547">Hallo zijn gewijzigde instellingen in Hallo-portal niet toegepast</span><span class="sxs-lookup"><span data-stu-id="3c6eb-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-548">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-548">Resolutions</span></span>
<span data-ttu-id="3c6eb-549">`omsconfig`Hallo configuration-agent in Hallo OMS-Agent is voor Linux die OMS-portal configuratiewijzigingen om de 5 minuten ophaalt.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="3c6eb-550">Deze configuratie wordt vervolgens toegepast toohello OMS-Agent voor Linux configuratiebestanden die zich bevindt op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="3c6eb-551">In sommige gevallen Hallo OMS-Agent voor Linux-agent voor configuratie mogelijk niet kunnen toocommunicate met Hallo portal configuration-service waardoor de meest recente configuratie niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="3c6eb-552">Controleer of deze Hallo `omsconfig` -agent is geïnstalleerd met de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="3c6eb-553">`dpkg --list omsconfig` of `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="3c6eb-554">Als niet geïnstalleerd, installeert u de nieuwste versie Hallo Hallo OMS-Agent voor Linux</span><span class="sxs-lookup"><span data-stu-id="3c6eb-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="3c6eb-555">Controleer of deze Hallo `omsconfig` agent kan communiceren met de Hallo OMS-service</span><span class="sxs-lookup"><span data-stu-id="3c6eb-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="3c6eb-556">Voer Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` opdracht</span><span class="sxs-lookup"><span data-stu-id="3c6eb-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="3c6eb-557">Hallo bovenstaande opdracht retourneert Hallo configuratie die agent opgehaald uit het Hallo-portal, met inbegrip van Syslog-instellingen, Linux-prestatiemeteritems en aangepaste logboeken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="3c6eb-558">Als bovenstaande Hallo-opdracht is mislukt, voert u Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="3c6eb-559">Met deze opdracht zorgt ervoor dat Hallo omsconfig agent toocommunicate met Hallo OMS service tooretrieve Hallo meest recente configuratie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="3c6eb-560">Aangepaste Linux-logboekgegevens niet wordt weergegeven in Hallo OMS-Portal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="3c6eb-561">Mogelijke oorzaken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-561">Probable causes</span></span>
* <span data-ttu-id="3c6eb-562">Onboarding tooOMS Service is mislukt</span><span class="sxs-lookup"><span data-stu-id="3c6eb-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="3c6eb-563">Hallo **toepassen Hallo na configuratie toomy Linux-Servers** instelling niet is geselecteerd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="3c6eb-564">omsconfig is niet opgenomen Hallo nieuwste aangepaste logboek van Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="3c6eb-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="3c6eb-565">Hallo `omsagent` gebruik is kan niet tooaccess Hallo aangepaste logboek vanwege een machtigingsprobleem tooa of `omsagent` is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="3c6eb-566">In dit geval ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="3c6eb-567">Dit is een bekend probleem met de Hallo Race Condition die in Hallo OMS-Agent voor Linux-versie 1.1.0-217 is opgelost</span><span class="sxs-lookup"><span data-stu-id="3c6eb-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3c6eb-568">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-568">Resolutions</span></span>
* <span data-ttu-id="3c6eb-569">Controleer of dat u geïmplementeerd, is hebt door te bepalen of hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bestand bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="3c6eb-570">Indien nodig, vrijgeven opnieuw met Hallo omsadmin.sh vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="3c6eb-571">Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="3c6eb-572">Hallo in OMS-Portal onder **instellingen** op Hallo **gegevens** tabblad, zorg ervoor dat Hallo **toepassen Hallo na configuratie toomy Linux-Servers** instelling is geselecteerd</span><span class="sxs-lookup"><span data-stu-id="3c6eb-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="3c6eb-573">![configuratie toepassen](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="3c6eb-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="3c6eb-574">Controleer of deze Hallo `omsconfig` agent kan communiceren met de Hallo OMS-service</span><span class="sxs-lookup"><span data-stu-id="3c6eb-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="3c6eb-575">Voer Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` opdracht</span><span class="sxs-lookup"><span data-stu-id="3c6eb-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="3c6eb-576">Hallo bovenstaande opdracht retourneert Hallo configuratie die agent opgehaald uit het Hallo-Portal, met inbegrip van Syslog-instellingen, Linux-prestatiemeteritems en aangepaste logboeken</span><span class="sxs-lookup"><span data-stu-id="3c6eb-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="3c6eb-577">Als bovenstaande Hallo-opdracht is mislukt, voert u Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="3c6eb-578">Deze opdracht forceert Hallo omsconfig agent toocommunicate met OMS-service en de meest recente configuratie Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="3c6eb-579">In plaats van Hallo OMS-Agent voor Linux-gebruiker wordt uitgevoerd als een bevoegde gebruiker `root`, Hallo OMS-Agent voor Linux wordt uitgevoerd als Hallo `omsagent` gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="3c6eb-580">In de meeste gevallen expliciete toestemming moet worden verleend toohello gebruiker in de volgorde tooread bepaalde bestanden.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="3c6eb-581">toogrant machtiging te`omsagent` gebruiker, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="3c6eb-582">Hallo toevoegen `omsagent` tooa specifieke gebruikersgroep met`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="3c6eb-583">Verleen leestoegang universal toohello vereist bestand met`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="3c6eb-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="3c6eb-584">Er is een bekend probleem met de Hallo Race Condition die in Hallo OMS-Agent voor Linux-versie 1.1.0-217 is opgelost.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="3c6eb-585">Voer na het bijwerken van de nieuwste agent toohello Hallo opdracht tooget Hallo meest recente versie van de uitvoer-invoegtoepassing Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c6eb-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="3c6eb-586">Bekende beperkingen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-586">Known limitations</span></span>
<span data-ttu-id="3c6eb-587">Bekijk Hallo toolearn secties over huidige beperkingen van Hallo OMS-Agent voor Linux te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="3c6eb-588">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="3c6eb-588">Azure Diagnostics</span></span>
<span data-ttu-id="3c6eb-589">Voor virtuele Linux-machines in Azure wordt uitgevoerd, mogelijk extra stappen vereist tooallow gegevensverzameling door Azure Diagnostics- en Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="3c6eb-590">**Versie 2.2** Hallo extensie voor diagnostische gegevens voor Linux is vereist voor compatibiliteit met Hallo OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="3c6eb-591">Zie voor meer informatie over het installeren en configureren van Hallo diagnostische extensie voor Linux [gebruiken hello Azure CLI opdracht tooenable Linux diagnostische extensie](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="3c6eb-592">**Upgraden 2.0 too2.2 Azure CLI ASM Hallo Linux-extensie voor diagnostische gegevens:**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="3c6eb-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="3c6eb-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="3c6eb-594">Deze opdrachtvoorbeelden verwijzen naar een bestand met de naam PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="3c6eb-595">Hallo-indeling van het bestand moet eruitzien als Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="3c6eb-596">Sysklog wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-596">Sysklog is not supported</span></span>
<span data-ttu-id="3c6eb-597">Rsyslog of syslog-ng zijn vereiste toocollect syslog-berichten.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="3c6eb-598">Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="3c6eb-599">toocollect syslog-gegevens van deze versie van deze verdelingen Hallo rsyslog daemon moet worden geïnstalleerd en geconfigureerd tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="3c6eb-600">Zie voor meer informatie over het vervangen van sysklog met rsyslog [Hallo zojuist gebouwd rsyslog RPM installeren](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="3c6eb-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c6eb-601">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c6eb-601">Next Steps</span></span>
* <span data-ttu-id="3c6eb-602">[Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="3c6eb-603">Raken met [Meld zoekopdrachten](log-analytics-log-searches.md) tooview gedetailleerde informatie verzameld door oplossingen.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="3c6eb-604">Gebruik [dashboards](log-analytics-dashboards.md) toosave en weergave van uw eigen aangepaste wordt gezocht.</span><span class="sxs-lookup"><span data-stu-id="3c6eb-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
