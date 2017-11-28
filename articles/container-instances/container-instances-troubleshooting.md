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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="1b294-103">Problemen met implementatie oplossen met Azure Containerexemplaren</span><span class="sxs-lookup"><span data-stu-id="1b294-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="1b294-104">Dit artikel laat zien hoe tootroubleshoot problemen bij het implementeren van containers tooAzure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="1b294-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="1b294-105">Ook wordt beschreven van Hallo voorkomende problemen die u kunt uitvoeren in.</span><span class="sxs-lookup"><span data-stu-id="1b294-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="1b294-106">Ophalen van diagnostische gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="1b294-106">Getting diagnostic events</span></span>

<span data-ttu-id="1b294-107">tooview logboeken van uw toepassingscode binnen een container, kunt u Hallo [az container logboeken](/cli/azure/container#logs) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1b294-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="1b294-108">Maar als de container niet met succes is geïmplementeerd, moet u tooreview Hallo diagnostische informatie door hello Azure Containerexemplaren resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="1b294-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="1b294-109">tooview hello gebeurtenissen voor de container, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1b294-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="1b294-110">Hallo uitvoer bevat Hallo core eigenschappen van de container, samen met de implementatie-gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="1b294-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="1b294-111">Algemene problemen bij de implementatie</span><span class="sxs-lookup"><span data-stu-id="1b294-111">Common deployment issues</span></span>

<span data-ttu-id="1b294-112">Er zijn een aantal veelvoorkomende problemen die account voor de meeste fouten in de implementatie.</span><span class="sxs-lookup"><span data-stu-id="1b294-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="1b294-113">Kan geen toopull afbeelding</span><span class="sxs-lookup"><span data-stu-id="1b294-113">Unable toopull image</span></span>

<span data-ttu-id="1b294-114">Als Azure Containerexemplaren niet kan toopull uw installatiekopie in eerste instantie wordt het opnieuw probeert gedurende een bepaalde voordat uiteindelijk mislukken.</span><span class="sxs-lookup"><span data-stu-id="1b294-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="1b294-115">Als het Hallo-installatiekopie kan niet worden opgehaald, worden gebeurtenissen, zoals Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="1b294-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

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

<span data-ttu-id="1b294-116">tooresolve, Hallo container verwijderen en probeer uw implementatie, betalende letten dat u de naam van de installatiekopie Hallo correct hebt getypt.</span><span class="sxs-lookup"><span data-stu-id="1b294-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="1b294-117">Container voortdurend wordt afgesloten en opnieuw wordt opgestart</span><span class="sxs-lookup"><span data-stu-id="1b294-117">Container continually exits and restarts</span></span>

<span data-ttu-id="1b294-118">Op dit moment ondersteunt Azure Containerexemplaren alleen langlopende services.</span><span class="sxs-lookup"><span data-stu-id="1b294-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="1b294-119">Als uw container wordt uitgevoerd toocompletion en zichzelf afsluit, het automatisch opnieuw wordt opgestart en wordt opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1b294-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="1b294-120">Als dit gebeurt, worden gebeurtenissen, zoals die na weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1b294-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="1b294-121">Houd er rekening mee dat Hallo-container kan worden gestart en vervolgens snel opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="1b294-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="1b294-122">Hallo Container exemplaren API bevat een `retryCount` eigenschap die laat zien hoe vaak een bepaalde container opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="1b294-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="1b294-123">Een shell, zoals bash, de meeste container afbeeldingen voor Linux-distributies ingesteld als Hallo standaardopdracht.</span><span class="sxs-lookup"><span data-stu-id="1b294-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="1b294-124">Aangezien een shell zelf geen langlopende service is, wordt deze containers onmiddellijk afsluiten en kunnen worden onderverdeeld in een lus opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="1b294-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="1b294-125">Container duurt een toostart lang</span><span class="sxs-lookup"><span data-stu-id="1b294-125">Container takes a long time toostart</span></span>

<span data-ttu-id="1b294-126">Als uw container een toostart lang duurt, maar uiteindelijk slaagt, eerst bekijkt hello grootte van de container-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="1b294-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="1b294-127">Omdat Azure Containerexemplaren de installatiekopie van de container op verzoek haalt, Hallo opstarttijd u ervaren is direct gerelateerd tooits grootte.</span><span class="sxs-lookup"><span data-stu-id="1b294-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="1b294-128">U kunt Hallo-grootte van de container-installatiekopie met behulp van Docker CLI Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="1b294-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="1b294-129">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="1b294-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="1b294-130">Hallo sleutel tookeeping grootte klein is ervoor zorgen dat dat de uiteindelijke installatiekopie bevat geen alles wat is niet vereist tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="1b294-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="1b294-131">Eenzijdige toodo dit met is [fasen builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="1b294-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="1b294-132">Meerdere fasen builds maken het gemakkelijk tooensure dat de uiteindelijke installatiekopie Hallo bevat alleen Hallo artefacten die u nodig hebt voor uw toepassing en niet een van de extra Hallo de inhoud die is vereist op build-tijd.</span><span class="sxs-lookup"><span data-stu-id="1b294-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="1b294-133">Hallo andere manier tooreduce Hallo Hallo installatiekopie pull op opstarten van de container heeft toohost Hallo container installatiekopie hello Azure Container register in Hallo met dezelfde regio waar u van plan toouse Azure Containerexemplaren bent.</span><span class="sxs-lookup"><span data-stu-id="1b294-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="1b294-134">Dit verkort Hallo netwerkpad dat Hallo container installatiekopie behoeften tootravel Hallo downloadtijd aanzienlijk verkorten.</span><span class="sxs-lookup"><span data-stu-id="1b294-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
