---
title: Gegevens verzamelen van CollectD in OMS Log Analytics | Microsoft Docs
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="b1e05-104">Gegevens verzamelen van CollectD op Linux-agents in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b1e05-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="b1e05-105">[CollectD](https://collectd.org/) is een open-source Linux-daemonwijzigingen die regelmatig maatstaven voor prestaties van toepassingen en het niveau van systeemgegevens verzamelt.</span><span class="sxs-lookup"><span data-stu-id="b1e05-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="b1e05-106">Voorbeeldtoepassingen bevatten de Java Virtual Machine (JVM), MySQL-Server en Nginx.</span><span class="sxs-lookup"><span data-stu-id="b1e05-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="b1e05-107">In dit artikel bevat informatie over het verzamelen van prestatiegegevens van CollectD in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="b1e05-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="b1e05-108">Een volledige lijst met beschikbare invoegtoepassingen kan worden gevonden op [tabel van invoegtoepassingen](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="b1e05-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Overzicht van CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="b1e05-110">De volgende CollectD-configuratie is opgenomen in de OMS-Agent voor Linux CollectD gegevens routeren naar de OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="b1e05-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="b1e05-111">Bovendien, als u een versie van collectD voordat 5.5 in plaats daarvan de volgende configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1e05-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="b1e05-112">De configuratie van de CollectD gebruikt de standaardinstallatielocatie`write_http` invoegtoepassing prestaties metrische gegevens verzenden via poort 26000 naar OMS-Agent voor Linux.</span><span class="sxs-lookup"><span data-stu-id="b1e05-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="b1e05-113">Deze poort kan worden geconfigureerd voor een aangepaste poort indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b1e05-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="b1e05-114">De OMS-Agent voor Linux ook luistert op poort 26000 voor CollectD metrische gegevens en converteert ze met OMS schema metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="b1e05-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="b1e05-115">Hieronder volgt de OMS-Agent voor Linux-configuratie `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="b1e05-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="b1e05-116">Ondersteunde versies van</span><span class="sxs-lookup"><span data-stu-id="b1e05-116">Versions supported</span></span>
- <span data-ttu-id="b1e05-117">Log Analytics ondersteunt momenteel CollectD versie 4.8 en hoger.</span><span class="sxs-lookup"><span data-stu-id="b1e05-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="b1e05-118">OMS-Agent voor Linux v1.1.0-217 of hoger is vereist voor CollectD metrische verzameling.</span><span class="sxs-lookup"><span data-stu-id="b1e05-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="b1e05-119">Configuratie</span><span class="sxs-lookup"><span data-stu-id="b1e05-119">Configuration</span></span>
<span data-ttu-id="b1e05-120">Hieronder vindt u eenvoudige stappen voor het verzamelen van gegevens CollectD configureren in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="b1e05-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="b1e05-121">CollectD om gegevens te verzenden naar de OMS-Agent voor Linux met behulp van de invoegtoepassing write_http configureren.</span><span class="sxs-lookup"><span data-stu-id="b1e05-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="b1e05-122">De OMS-Agent voor Linux te luisteren naar de CollectD gegevens op de juiste poort configureren.</span><span class="sxs-lookup"><span data-stu-id="b1e05-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="b1e05-123">CollectD en OMS-Agent voor Linux opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="b1e05-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="b1e05-124">CollectD voor het doorsturen van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="b1e05-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="b1e05-125">Gegevens van de CollectD routeren naar de OMS-Agent voor Linux `oms.conf` moet worden toegevoegd aan de configuratiemap van CollectD.</span><span class="sxs-lookup"><span data-stu-id="b1e05-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="b1e05-126">Het doel van dit bestand is afhankelijk van de Linux-distro van uw machine.</span><span class="sxs-lookup"><span data-stu-id="b1e05-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="b1e05-127">Als uw CollectD config directory bevindt zich in /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="b1e05-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="b1e05-128">Als uw CollectD config directory bevindt zich in /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="b1e05-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="b1e05-129">Voor versies van CollectD voor 5.5 u moet de labels in wijzigen `oms.conf` zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="b1e05-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="b1e05-130">Kopieer collectd.conf naar de gewenste werkruimte omsagent configuratiemap.</span><span class="sxs-lookup"><span data-stu-id="b1e05-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="b1e05-131">Start CollectD en OMS-Agent voor Linux opnieuw met de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="b1e05-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="b1e05-132">sudo service collectd sudo /opt/microsoft/omsagent/bin/service_control opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="b1e05-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="b1e05-133">CollectD metrische gegevens voor de conversie van logboekanalyse schema</span><span class="sxs-lookup"><span data-stu-id="b1e05-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="b1e05-134">Voor het onderhouden van een vertrouwde model tussen infrastructuur metrische gegevens die al zijn verzameld door de OMS-Agent voor Linux en de nieuwe metrische gegevens die worden verzameld door CollectD de volgende schematoewijzing wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="b1e05-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="b1e05-135">CollectD metriek veld</span><span class="sxs-lookup"><span data-stu-id="b1e05-135">CollectD Metric field</span></span> | <span data-ttu-id="b1e05-136">Log Analytics-veld</span><span class="sxs-lookup"><span data-stu-id="b1e05-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="b1e05-137">host</span><span class="sxs-lookup"><span data-stu-id="b1e05-137">host</span></span> | <span data-ttu-id="b1e05-138">Computer</span><span class="sxs-lookup"><span data-stu-id="b1e05-138">Computer</span></span> |
| <span data-ttu-id="b1e05-139">Invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="b1e05-139">plugin</span></span> | <span data-ttu-id="b1e05-140">Geen</span><span class="sxs-lookup"><span data-stu-id="b1e05-140">None</span></span> |
| <span data-ttu-id="b1e05-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="b1e05-141">plugin_instance</span></span> | <span data-ttu-id="b1e05-142">Exemplaarnaam</span><span class="sxs-lookup"><span data-stu-id="b1e05-142">Instance Name</span></span><br><span data-ttu-id="b1e05-143">Als **plugin_instance** is *null* vervolgens InstanceName = "*_Totaal*'</span><span class="sxs-lookup"><span data-stu-id="b1e05-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="b1e05-144">type</span><span class="sxs-lookup"><span data-stu-id="b1e05-144">type</span></span> | <span data-ttu-id="b1e05-145">Objectnaam</span><span class="sxs-lookup"><span data-stu-id="b1e05-145">ObjectName</span></span> |
| <span data-ttu-id="b1e05-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="b1e05-146">type_instance</span></span> | <span data-ttu-id="b1e05-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="b1e05-147">CounterName</span></span><br><span data-ttu-id="b1e05-148">Als **type_instance** is *null* vervolgens CounterName =**leeg**</span><span class="sxs-lookup"><span data-stu-id="b1e05-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="b1e05-149">dsnames]</span><span class="sxs-lookup"><span data-stu-id="b1e05-149">dsnames[]</span></span> | <span data-ttu-id="b1e05-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="b1e05-150">CounterName</span></span> |
| <span data-ttu-id="b1e05-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="b1e05-151">dstypes</span></span> | <span data-ttu-id="b1e05-152">Geen</span><span class="sxs-lookup"><span data-stu-id="b1e05-152">None</span></span> |
| <span data-ttu-id="b1e05-153">[] waarden</span><span class="sxs-lookup"><span data-stu-id="b1e05-153">values[]</span></span> | <span data-ttu-id="b1e05-154">Tegenwaarde</span><span class="sxs-lookup"><span data-stu-id="b1e05-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b1e05-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1e05-155">Next steps</span></span>
* <span data-ttu-id="b1e05-156">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) om de gegevens verzameld van gegevensbronnen en oplossingen te analyseren.</span><span class="sxs-lookup"><span data-stu-id="b1e05-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="b1e05-157">Gebruik [aangepaste velden](log-analytics-custom-fields.md) parseren van gegevens van syslog-records in afzonderlijke velden.</span><span class="sxs-lookup"><span data-stu-id="b1e05-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

