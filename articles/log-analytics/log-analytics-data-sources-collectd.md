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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Gegevens verzamelen van CollectD op Linux-agents in Log Analytics
[CollectD](https://collectd.org/) is een open-source Linux-daemonwijzigingen die regelmatig maatstaven voor prestaties van toepassingen en het niveau van systeemgegevens verzamelt. Van de voorbeeldtoepassingen zijn Hallo Java Virtual Machine (JVM), MySQL-Server en Nginx. In dit artikel bevat informatie over het verzamelen van prestatiegegevens van CollectD in logboekanalyse.

Een volledige lijst met beschikbare invoegtoepassingen kan worden gevonden op [tabel van invoegtoepassingen](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Overzicht van CollectD](media/log-analytics-data-sources-collectd/overview.png)

Hallo is volgende CollectD configuratie opgenomen in Hallo OMS-Agent voor Linux tooroute CollectD gegevens toohello OMS-Agent voor Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Bovendien, als u een versie van collectD voordat 5.5 Hallo na configuratie in plaats daarvan gebruikt.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

Hallo CollectD configuratie maakt gebruik van standaard Hallo`write_http` invoegtoepassing toosend prestaties metrische gegevens via poort 26000 tooOMS Agent voor Linux. 

> [!NOTE]
> Deze poort kan geconfigureerde tooa aangepaste poort zijn, indien nodig.

Hallo OMS-Agent voor Linux ook luistert op poort 26000 voor CollectD metrische gegevens en zet deze tooOMS schema metrische gegevens. Hallo volgt Hallo OMS-Agent voor Linux-configuratie `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Ondersteunde versies van
- Log Analytics ondersteunt momenteel CollectD versie 4.8 en hoger.
- OMS-Agent voor Linux v1.1.0-217 of hoger is vereist voor CollectD metrische verzameling.


## <a name="configuration"></a>Configuratie
Hallo hieronder vindt u eenvoudige stappen tooconfigure verzamelen van gegevens van de CollectD in logboekanalyse.

1. CollectD toosend gegevens toohello OMS-Agent voor Linux met Hallo write_http-invoegtoepassing configureren.  
2. Hallo OMS-Agent voor Linux-toolisten voor Hallo CollectD gegevens op de juiste poort Hallo configureren.
3. CollectD en OMS-Agent voor Linux opnieuw gestart.

### <a name="configure-collectd-tooforward-data"></a>CollectD tooforward gegevens configureren 

1. tooroute CollectD gegevens toohello OMS-Agent voor Linux `oms.conf` behoeften toobe van tooCollectD configuratiemap toegevoegd. Hallo-doel van dit bestand is afhankelijk van Hallo Linux distro van uw machine.

    Als uw CollectD config directory bevindt zich in /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Als uw CollectD config directory bevindt zich in /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Voor versies van CollectD voor 5.5 hebt uitgevoerd, toomodify Hallo labels `oms.conf` zoals hierboven.
    >

2. Kopieer collectd.conf toohello gewenst werkruimte omsagent configuratiemap.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. En opnieuw gestart CollectD OMS-Agent voor Linux Hello opdrachten te volgen.

    sudo service collectd sudo /opt/microsoft/omsagent/bin/service_control opnieuw starten

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD metrische gegevens tooLog Analytics schema conversie
toomaintain een vertrouwde model tussen infrastructuur metrische gegevens die al zijn verzameld door de OMS-Agent voor Linux- en Hallo nieuwe metrische gegevens die worden verzameld door CollectD Hallo schematoewijzing volgende wordt gebruikt:

| CollectD metriek veld | Log Analytics-veld |
|:--|:--|
| host | Computer |
| Invoegtoepassing | Geen |
| plugin_instance | Exemplaarnaam<br>Als **plugin_instance** is *null* vervolgens InstanceName = "*_Totaal*' |
| type | Objectnaam |
| type_instance | CounterName<br>Als **type_instance** is *null* vervolgens CounterName =**leeg** |
| dsnames] | CounterName |
| dstypes | Geen |
| [] waarden | Tegenwaarde |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen. 
* Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse gegevens van syslog-records in afzonderlijke velden.

