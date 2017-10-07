---
title: aaaManage Azure DC/OS-cluster met Marathon REST API | Microsoft Docs
description: Containers tooan Azure Container Service DC/OS-cluster implementeren met behulp van Hallo Marathon REST API.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>DC/OS-containerbeheer via Hallo Marathon REST API
DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde werkbelastingen terwijl het Hallo onderliggende hardware wordt onttrokken. Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt. Er zijn frameworks beschikbaar voor veel populaire werkbelastingen, wordt er in dit document helpt u op weg maken en schalen van containerimplementaties met behulp van Hallo Marathon REST API. 

## <a name="prerequisites"></a>Vereisten

Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service. U moet ook toohave externe connectiviteit toothis cluster. Zie voor meer informatie over deze items Hallo artikelen te volgen:

* [Een Azure Container Service-cluster implementeren](container-service-deployment.md)
* [Verbinding maken met tooan Azure Container Service-cluster](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Toegang tot Hallo DC/OS-API 's
Nadat u verbonden toohello Azure Container Service-cluster bent, kunt u via http://localhost: Local-port Hallo DC/OS en gerelateerde REST-API's openen. Hallo-voorbeelden in dit document wordt ervan uitgegaan dat u via tunneling op poort 80. Bijvoorbeeld, Hallo Marathon-eindpunten op URI's kunnen worden bereikt vanaf `http://localhost/marathon/v2/`. 

Verschillende API's, Zie voor meer informatie op Hallo Hallo Mesosphere-documentatie voor Hallo [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) en de [Chronos API](https://mesos.github.io/chronos/docs/api.html), en de Apache-documentatie voor Hallo [Mesos Scheduler API ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Informatie verzamelen van DC/OS en Marathon
Voordat u containers toohello DC/OS-cluster implementeert, verzamelt u wat informatie over Hallo DC/OS-cluster, zoals Hallo namen en status van Hallo DC/OS-agents. toodo query dus Hallo `master/slaves` eindpunt Hallo DC/OS REST-API. Als alles goed gaat, retourneert Hallo query een lijst van DC/OS-agents en de verschillende eigenschappen voor elk.

```bash
curl http://localhost/mesos/master/slaves
```

Nu gebruiken Hallo Marathon `/apps` toocheck eindpunt voor de huidige toepassing implementaties toohello DC/OS-cluster. Als dit een nieuw cluster is, ziet u een lege matrix voor apps.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Een met Docker ingedeelde container implementeren
U kunt Docker ingedeelde containers via Marathon REST API Hallo implementeren met behulp van een JSON-bestand die Hallo bedoeld implementatie beschrijft. Hallo implementeert volgende voorbeeld een Nginx-container tooa persoonlijke agent in Hallo-cluster. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

Hallo JSON-bestand toodeploy een met Docker ingedeelde container, opslaan in een toegankelijke locatie. Vervolgens toodeploy Hallo-container, Hallo volgende opdracht uitvoeren. Hallo naam opgeven van Hallo JSON-bestand (`marathon.json` in dit voorbeeld).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

Hallo-uitvoer is vergelijkbaar toohello volgende:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Nu, als u een query Marathon voor toepassingen uitvoert, deze nieuwe toepassing wordt weergegeven in Hallo uitvoer.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Hallo-container bereiken

U kunt die Nginx wordt uitgevoerd in een container op een van de persoonlijke agents in het cluster Hallo HALLO hallo controleren. toofind hello host en poort waarop Hallo container wordt uitgevoerd, doorzoeken Marathon Hallo actieve taken: 

```bash
curl localhost/marathon/v2/tasks
```

Hallo-waarde van zoeken `host` in Hallo uitvoer (een IP-adres te vergelijkbare`10.32.0.x`), en de waarde van Hallo `ports`.


Maak nu een SSH terminal-verbinding (niet via een tunnel verbinding) toohello management FQDN-naam van Hallo cluster. Eenmaal zijn verbonden, zorg Hallo aanvraag te volgen, vervangen door de juiste waarden Hallo van `host` en `ports`:

```bash
curl http://host:ports
```

Hallo Nginx server-uitvoer is vergelijkbaar toohello volgende:

![Nginx van container](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Uw containers schalen
U kunt Hallo Marathon API tooscale out- of schaal gebruiken in implementaties van toepassingen. In het vorige voorbeeld hello, moet u een exemplaar van een toepassing geïmplementeerd. Schalen we dit uit toothree exemplaren van een toepassing. toodo dus een JSON-bestand maken met behulp van de volgende JSON-tekst hello en sla deze op een toegankelijke locatie.

```json
{ "instances": 3 }
```

Uitvoeren van uw verbinding via een tunnel, Hallo opdracht tooscale uit de toepassing hello te volgen.

> [!NOTE]
> Hallo-URI is http://localhost/marathon/v2/apps/ gevolgd door het Hallo-ID van Hallo toepassing tooscale. Als u van Hallo Nginx-voorbeeld gebruikt die is opgegeven hier gebruikmaakt, zou Hallo URI http://localhost/marathon/v2/apps/nginx zijn.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Voer tenslotte een query Hallo Marathon-eindpunt voor toepassingen. U zult zien dat er nu drie Nginx-containers zijn.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Vergelijkbare PowerShell-opdrachten
U kunt dezelfde acties uitvoeren met behulp van PowerShell-opdrachten in een Windows-systeem.

toogather informatie over Hallo DC/OS-cluster, zoals agentnamen en agentstatus, Hallo volgende opdracht uitvoeren:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

U kunt Docker ingedeelde containers via Marathon implementeren met behulp van een JSON-bestand die Hallo bedoeld implementatie beschrijft. Hallo implementeert volgende voorbeeld Hallo Nginx-container, binding van poort 80 van Hallo DC/OS-agent tooport 80 van Hallo-container.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

Hallo JSON-bestand toodeploy een met Docker ingedeelde container, opslaan in een toegankelijke locatie. Vervolgens toodeploy Hallo-container, Hallo volgende opdracht uitvoeren. Geef Hallo pad toohello JSON-bestand (`marathon.json` in dit voorbeeld).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

U kunt ook Hallo Marathon API tooscale out- of schaal gebruiken in implementaties van toepassingen. In het vorige voorbeeld hello, moet u een exemplaar van een toepassing geïmplementeerd. Schalen we dit uit toothree exemplaren van een toepassing. toodo dus een JSON-bestand maken met behulp van de volgende JSON-tekst hello en sla deze op een toegankelijke locatie.

```json
{ "instances": 3 }
```

Voer Hallo opdracht tooscale uit de toepassing hello te volgen:

> [!NOTE]
> Hallo-URI is http://localhost/marathon/v2/apps/ gevolgd door het Hallo-ID van Hallo toepassing tooscale. Als u van Hallo Nginx-voorbeeld opgegeven hier gebruikmaakt, zou Hallo URI http://localhost/marathon/v2/apps/nginx zijn.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Volgende stappen
* [Lees meer over Hallo Mesos HTTP-eindpunten](http://mesos.apache.org/documentation/latest/endpoints/)
* [Lees meer over Hallo Marathon REST API](https://mesosphere.github.io/marathon/docs/rest-api.html)

