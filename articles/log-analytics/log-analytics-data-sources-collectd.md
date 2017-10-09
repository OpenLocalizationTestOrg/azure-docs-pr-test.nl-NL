---
title: aaaCollect gegevens van CollectD in OMS Log Analytics | Microsoft Docs
description: CollectD is een open-source Linux-daemonwijzigingen waarmee periodiek gegevens worden verzameld van toepassingen en het niveau van systeemgegevens.  In dit artikel bevat informatie over het verzamelen van gegevens van CollectD in logboekanalyse.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="a4b0a-104">Gegevens verzamelen van CollectD op Linux-agents in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a4b0a-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="a4b0a-105">[CollectD](https://collectd.org/) is een open-source Linux-daemonwijzigingen die regelmatig maatstaven voor prestaties van toepassingen en het niveau van systeemgegevens verzamelt.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="a4b0a-106">Van de voorbeeldtoepassingen zijn Hallo Java Virtual Machine (JVM), MySQL-Server en Nginx.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="a4b0a-107">In dit artikel bevat informatie over het verzamelen van prestatiegegevens van CollectD in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="a4b0a-108">Een volledige lijst met beschikbare invoegtoepassingen kan worden gevonden op [tabel van invoegtoepassingen](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="a4b0a-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Overzicht van CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="a4b0a-110">Hallo is volgende CollectD configuratie opgenomen in Hallo OMS-Agent voor Linux tooroute CollectD gegevens toohello OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="a4b0a-111">Bovendien, als u een versie van collectD voordat 5.5 Hallo na configuratie in plaats daarvan gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="a4b0a-112">Hallo CollectD configuratie maakt gebruik van standaard Hallo`write_http` invoegtoepassing toosend prestaties metrische gegevens via poort 26000 tooOMS Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4b0a-113">Deze poort kan geconfigureerde tooa aangepaste poort zijn, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="a4b0a-114">Hallo OMS-Agent voor Linux ook luistert op poort 26000 voor CollectD metrische gegevens en zet deze tooOMS schema metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="a4b0a-115">Hallo volgt Hallo OMS-Agent voor Linux-configuratie `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="a4b0a-116">Ondersteunde versies van</span><span class="sxs-lookup"><span data-stu-id="a4b0a-116">Versions supported</span></span>
- <span data-ttu-id="a4b0a-117">Log Analytics ondersteunt momenteel CollectD versie 4.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="a4b0a-118">OMS-Agent voor Linux v1.1.0-217 of hoger is vereist voor CollectD metrische verzameling.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="a4b0a-119">Configuratie</span><span class="sxs-lookup"><span data-stu-id="a4b0a-119">Configuration</span></span>
<span data-ttu-id="a4b0a-120">Hallo hieronder vindt u eenvoudige stappen tooconfigure verzamelen van gegevens van de CollectD in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="a4b0a-121">CollectD toosend gegevens toohello OMS-Agent voor Linux met Hallo write_http-invoegtoepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="a4b0a-122">Hallo OMS-Agent voor Linux-toolisten voor Hallo CollectD gegevens op de juiste poort Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="a4b0a-123">CollectD en OMS-Agent voor Linux opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="a4b0a-124">CollectD tooforward gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="a4b0a-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="a4b0a-125">tooroute CollectD gegevens toohello OMS-Agent voor Linux `oms.conf` behoeften toobe van tooCollectD configuratiemap toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="a4b0a-126">Hallo-doel van dit bestand is afhankelijk van Hallo Linux distro van uw machine.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="a4b0a-127">Als uw CollectD config directory bevindt zich in /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="a4b0a-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="a4b0a-128">Als uw CollectD config directory bevindt zich in /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="a4b0a-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="a4b0a-129">Voor versies van CollectD voor 5.5 hebt uitgevoerd, toomodify Hallo labels `oms.conf` zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="a4b0a-130">Kopieer collectd.conf toohello gewenst werkruimte omsagent configuratiemap.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="a4b0a-131">En opnieuw gestart CollectD OMS-Agent voor Linux Hello opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="a4b0a-132">sudo service collectd sudo /opt/microsoft/omsagent/bin/service_control opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="a4b0a-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="a4b0a-133">CollectD metrische gegevens tooLog Analytics schema conversie</span><span class="sxs-lookup"><span data-stu-id="a4b0a-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="a4b0a-134">toomaintain een vertrouwde model tussen infrastructuur metrische gegevens die al zijn verzameld door de OMS-Agent voor Linux- en Hallo nieuwe metrische gegevens die worden verzameld door CollectD Hallo schematoewijzing volgende wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="a4b0a-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="a4b0a-135">CollectD metriek veld</span><span class="sxs-lookup"><span data-stu-id="a4b0a-135">CollectD Metric field</span></span> | <span data-ttu-id="a4b0a-136">Log Analytics-veld</span><span class="sxs-lookup"><span data-stu-id="a4b0a-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="a4b0a-137">host</span><span class="sxs-lookup"><span data-stu-id="a4b0a-137">host</span></span> | <span data-ttu-id="a4b0a-138">Computer</span><span class="sxs-lookup"><span data-stu-id="a4b0a-138">Computer</span></span> |
| <span data-ttu-id="a4b0a-139">Invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="a4b0a-139">plugin</span></span> | <span data-ttu-id="a4b0a-140">Geen</span><span class="sxs-lookup"><span data-stu-id="a4b0a-140">None</span></span> |
| <span data-ttu-id="a4b0a-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="a4b0a-141">plugin_instance</span></span> | <span data-ttu-id="a4b0a-142">Exemplaarnaam</span><span class="sxs-lookup"><span data-stu-id="a4b0a-142">Instance Name</span></span><br><span data-ttu-id="a4b0a-143">Als **plugin_instance** is *null* vervolgens InstanceName = "*_Totaal*'</span><span class="sxs-lookup"><span data-stu-id="a4b0a-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="a4b0a-144">type</span><span class="sxs-lookup"><span data-stu-id="a4b0a-144">type</span></span> | <span data-ttu-id="a4b0a-145">Objectnaam</span><span class="sxs-lookup"><span data-stu-id="a4b0a-145">ObjectName</span></span> |
| <span data-ttu-id="a4b0a-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="a4b0a-146">type_instance</span></span> | <span data-ttu-id="a4b0a-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="a4b0a-147">CounterName</span></span><br><span data-ttu-id="a4b0a-148">Als **type_instance** is *null* vervolgens CounterName =**leeg**</span><span class="sxs-lookup"><span data-stu-id="a4b0a-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="a4b0a-149">dsnames]</span><span class="sxs-lookup"><span data-stu-id="a4b0a-149">dsnames[]</span></span> | <span data-ttu-id="a4b0a-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="a4b0a-150">CounterName</span></span> |
| <span data-ttu-id="a4b0a-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="a4b0a-151">dstypes</span></span> | <span data-ttu-id="a4b0a-152">Geen</span><span class="sxs-lookup"><span data-stu-id="a4b0a-152">None</span></span> |
| <span data-ttu-id="a4b0a-153">[] waarden</span><span class="sxs-lookup"><span data-stu-id="a4b0a-153">values[]</span></span> | <span data-ttu-id="a4b0a-154">Tegenwaarde</span><span class="sxs-lookup"><span data-stu-id="a4b0a-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a4b0a-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4b0a-155">Next steps</span></span>
* <span data-ttu-id="a4b0a-156">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="a4b0a-157">Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse gegevens van syslog-records in afzonderlijke velden.</span><span class="sxs-lookup"><span data-stu-id="a4b0a-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

