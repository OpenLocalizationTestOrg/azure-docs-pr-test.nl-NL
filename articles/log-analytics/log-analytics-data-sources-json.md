---
title: aangepaste JSON-gegevens aaaCollecting in OMS Log Analytics | Microsoft Docs
description: Aangepaste JSON-gegevensbronnen kunnen worden verzameld in Hallo OMS-Agent voor Linux met logboekanalyse.  Deze aangepaste gegevensbronnen mag eenvoudige scripts JSON zoals curl of een van de FluentD 300 + plugins retourneren. Dit artikel wordt beschreven Hallo-configuratie vereist om deze gegevens te verzamelen.
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Verzamelen van aangepaste JSON-gegevensbronnen Hello OMS-Agent voor Linux in Log Analytics
Aangepaste JSON-gegevensbronnen kunnen worden verzameld in Hallo OMS-Agent voor Linux met logboekanalyse.  Deze aangepaste gegevensbronnen kunnen worden eenvoudige scripts JSON zoals retourneren [curl](https://curl.haxx.se/) of een van [FluentD van 300 + plugins](http://www.fluentd.org/plugins/all). Dit artikel wordt beschreven Hallo-configuratie vereist om deze gegevens te verzamelen.

> [!NOTE]
> OMS-Agent voor Linux v1.1.0-217 + is vereist voor de aangepaste JSON-gegevens

## <a name="configuration"></a>Configuratie

### <a name="configure-input-plugin"></a>Invoer-invoegtoepassing configureren

toevoegen van JSON-gegevens in Log Analytics toocollect `oms.api.` toohello begin van een label FluentD in een invoegtoepassing voor invoer.

Volgende is bijvoorbeeld een afzonderlijk configuratiebestand `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Dit maakt gebruik van Hallo FluentD invoegtoepassing `exec` toorun een curl-opdracht elke 30 seconden.  Hallo-uitvoer van deze opdracht worden verzameld door Hallo JSON-uitvoer invoegtoepassing.

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
Hallo-configuratiebestand toegevoegd onder `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` toohave eigendom ervan is gewijzigd met de volgende opdracht Hallo is vereist.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Output-invoegtoepassing configureren 
Hallo na uitvoer-invoegtoepassing configuration toohello belangrijkste configuratie in toevoegen `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` of als een afzonderlijk configuratiebestand in geplaatst`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a>Opnieuw opstarten OMS-Agent voor Linux
Hallo OMS-Agent voor Linux-service met de volgende opdracht Hallo opnieuw opstarten

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Uitvoer
Hallo-gegevens worden verzameld in logboekanalyse met een recordtype van `<FLUENTD_TAG>_CL`.

Bijvoorbeeld, Hallo aangepaste label `tag oms.api.tomcat` in logboekanalyse met een recordtype van `tomcat_CL`.  Alle records van dit type kan worden opgehaald met Hallo logboek zoeken te volgen.

    Type=tomcat_CL

Geneste JSON-gegevens bronnen worden ondersteund, maar zijn geïndexeerd gebaseerd op de bovenliggende veld. Bijvoorbeeld, Hallo volgende JSON-gegevens geretourneerd van een zoekopdracht logboekanalyse als `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen. 
 