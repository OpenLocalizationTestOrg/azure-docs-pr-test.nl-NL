---
title: aaaTroubleshooting exemplaren van Azure-Container
description: Meer informatie over hoe tootroubleshoot problemen met een Azure Containerexemplaren
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Problemen met implementatie oplossen met Azure Containerexemplaren

Dit artikel laat zien hoe tootroubleshoot problemen bij het implementeren van containers tooAzure Containerexemplaren. Ook wordt beschreven van Hallo voorkomende problemen die u kunt uitvoeren in.

## <a name="getting-diagnostic-events"></a>Ophalen van diagnostische gebeurtenissen

tooview logboeken van uw toepassingscode binnen een container, kunt u Hallo [az container logboeken](/cli/azure/container#logs) opdracht. Maar als de container niet met succes is geïmplementeerd, moet u tooreview Hallo diagnostische informatie door hello Azure Containerexemplaren resourceprovider. tooview hello gebeurtenissen voor de container, Hallo volgende opdracht uitvoeren:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

Hallo uitvoer bevat Hallo core eigenschappen van de container, samen met de implementatie-gebeurtenissen:

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>Algemene problemen bij de implementatie

Er zijn een aantal veelvoorkomende problemen die account voor de meeste fouten in de implementatie.

### <a name="unable-toopull-image"></a>Kan geen toopull afbeelding

Als Azure Containerexemplaren niet kan toopull uw installatiekopie in eerste instantie wordt het opnieuw probeert gedurende een bepaalde voordat uiteindelijk mislukken. Als het Hallo-installatiekopie kan niet worden opgehaald, worden gebeurtenissen, zoals Hallo volgende weergegeven:

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, Hallo container verwijderen en probeer uw implementatie, betalende letten dat u de naam van de installatiekopie Hallo correct hebt getypt.

### <a name="container-continually-exits-and-restarts"></a>Container voortdurend wordt afgesloten en opnieuw wordt opgestart

Op dit moment ondersteunt Azure Containerexemplaren alleen langlopende services. Als uw container wordt uitgevoerd toocompletion en zichzelf afsluit, het automatisch opnieuw wordt opgestart en wordt opnieuw uitgevoerd. Als dit gebeurt, worden gebeurtenissen, zoals die na weergegeven. Houd er rekening mee dat Hallo-container kan worden gestart en vervolgens snel opnieuw wordt opgestart. Hallo Container exemplaren API bevat een `retryCount` eigenschap die laat zien hoe vaak een bepaalde container opnieuw is opgestart.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> Een shell, zoals bash, de meeste container afbeeldingen voor Linux-distributies ingesteld als Hallo standaardopdracht. Aangezien een shell zelf geen langlopende service is, wordt deze containers onmiddellijk afsluiten en kunnen worden onderverdeeld in een lus opnieuw opstarten.

### <a name="container-takes-a-long-time-toostart"></a>Container duurt een toostart lang

Als uw container een toostart lang duurt, maar uiteindelijk slaagt, eerst bekijkt hello grootte van de container-installatiekopie. Omdat Azure Containerexemplaren de installatiekopie van de container op verzoek haalt, Hallo opstarttijd u ervaren is direct gerelateerd tooits grootte.

U kunt Hallo-grootte van de container-installatiekopie met behulp van Docker CLI Hallo bekijken:

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

Hallo sleutel tookeeping grootte klein is ervoor zorgen dat dat de uiteindelijke installatiekopie bevat geen alles wat is niet vereist tijdens runtime. Eenzijdige toodo dit met is [fasen builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Meerdere fasen builds maken het gemakkelijk tooensure dat de uiteindelijke installatiekopie Hallo bevat alleen Hallo artefacten die u nodig hebt voor uw toepassing en niet een van de extra Hallo de inhoud die is vereist op build-tijd.

Hallo andere manier tooreduce Hallo Hallo installatiekopie pull op opstarten van de container heeft toohost Hallo container installatiekopie hello Azure Container register in Hallo met dezelfde regio waar u van plan toouse Azure Containerexemplaren bent. Dit verkort Hallo netwerkpad dat Hallo container installatiekopie behoeften tootravel Hallo downloadtijd aanzienlijk verkorten.
