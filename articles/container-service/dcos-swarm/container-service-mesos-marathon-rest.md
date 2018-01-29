---
title: Azure DC/OS-cluster met Marathon REST API beheren
description: Implementeer containers naar een Azure Container Service DC/OS-cluster met behulp van de Marathon REST API.
services: container-service
author: dlepow
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c9322756c30011305ebe6f4f2fd38554f275a1b3
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/06/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a>DC/OS-containerbeheer via de Marathon REST API

DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde workloads terwijl de onderliggende hardware wordt onttrokken. Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt. Er zijn frameworks beschikbaar voor veel populaire werkbelastingen, wordt er in dit document helpt u op weg maken en schalen van containerimplementaties met behulp van de Marathon REST API. 

## <a name="prerequisites"></a>Vereisten

Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service. U hebt ook een externe verbinding met dit cluster nodig. Zie de volgende artikelen voor meer informatie over deze items:

* [Een Azure Container Service-cluster implementeren](container-service-deployment.md)
* [Verbinding maken met een Azure Container Service-cluster](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a>Toegang tot de DC/OS-API 's
Nadat u met het Azure Container Service-cluster bent verbonden, hebt u via http://localhost:local-port toegang tot DC/OS en gerelateerde REST API's. In de voorbeelden in dit document wordt ervan uitgegaan dat u poort 80 gebruikt. Bijvoorbeeld, de Marathon-eindpunten op URI's kunnen worden bereikt vanaf `http://localhost/marathon/v2/`. 

Zie voor meer informatie over de verschillende API's de Mesosphere-documentatie voor de [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) en de [Chronos API](https://mesos.github.io/chronos/docs/api.html), en de Apache-documentatie voor de [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Informatie verzamelen van DC/OS en Marathon
Voordat u containers naar het DC/OS-cluster implementeert, verzamelt u wat informatie over het DC/OS-cluster, zoals de namen en de status van de DC/OS-agents. U doet dit door een query uit te voeren op het `master/slaves`-eindpunt van de DC/OS REST API. Als alles goed gaat, wordt met de query een lijst geretourneerd van DC/OS-agents en de verschillende eigenschappen voor elke agent.

```bash
curl http://localhost/mesos/master/slaves
```

Gebruik nu het Marathon `/apps`-eindpunt om te controleren op huidige implementaties naar het DC/OS-cluster. Als dit een nieuw cluster is, ziet u een lege matrix voor apps.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Een met Docker ingedeelde container implementeren
U kunt Docker ingedeelde containers via Marathon REST-API implementeren met behulp van een JSON-bestand dat het doel van de implementatie beschrijft. Het volgende voorbeeld wordt een Nginx-container geïmplementeerd naar een persoonlijke agent in het cluster. 

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

Sla het JSON-bestand op een toegankelijke locatie voor het implementeren van een met Docker ingedeelde container. Voer vervolgens de volgende opdracht uit om de container te implementeren Geef de naam van het JSON-bestand (`marathon.json` in dit voorbeeld).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

De uitvoer lijkt op het volgende:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Als u in Marathon toepassingen opvraagt via een query, wordt deze nieuwe toepassing in de uitvoer weergegeven.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a>De container bereiken

U kunt controleren of de Nginx wordt uitgevoerd in een container op een van de persoonlijke agents in het cluster. Als u wilt zoeken op de host en de poort waarop de container wordt uitgevoerd, query Marathon voor actieve taken: 

```bash
curl localhost/marathon/v2/tasks
```

De waarde van zoeken `host` in de uitvoer (een IP-adres dat lijkt op `10.32.0.x`), en de waarde van `ports`.


Nu een terminal SSH-verbinding (niet via een tunnel verbinding) aanbrengen in de management FQDN-naam van het cluster. Eenmaal zijn verbonden, maken de volgende aanvraag, vervangen door de juiste waarden van `host` en `ports`:

```bash
curl http://host:ports
```

De uitvoer van de server Nginx is vergelijkbaar met het volgende:

![Nginx van container](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Uw containers schalen
U kunt de Marathon API uitbreiden of schalen in implementaties van toepassingen. In het vorige voorbeeld hebt u één exemplaar van een toepassing geïmplementeerd. Laten we dit uitschalen naar drie exemplaren van een toepassing. Dit doet u door een JSON-bestand te maken met behulp van de volgende JSON-tekst en dit op een toegankelijke locatie op te slaan.

```json
{ "instances": 3 }
```

Voer de volgende opdracht uit de toepassing te schalen van uw via een tunnel verbinding.

> [!NOTE]
> De URI is http://localhost/marathon/v2/apps/ gevolgd door de id van de toepassing die u wilt schalen. Als u het Nginx-voorbeeld gebruikt dat hier wordt besproken, zou de URI http://localhost/marathon/v2/apps/nginx zijn.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Voer tenslotte een query voor toepassingen uit op het Marathon-eindpunt. U zult zien dat er nu drie Nginx-containers zijn.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Vergelijkbare PowerShell-opdrachten
U kunt dezelfde acties uitvoeren met behulp van PowerShell-opdrachten in een Windows-systeem.

Voor het verzamelen van informatie over het DC/OS-cluster, zoals agentnamen en agentstatus, voer de volgende opdracht:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

U implementeert met Docker ingedeelde containers via Marathon met behulp van een JSON-bestand waarin het doel van de implementatie wordt beschreven. In het volgende voorbeeld wordt de Nginx-container geïmplementeerd, met een binding van poort 80 van de DC/OS-agent naar poort 80 van de container.

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

Sla het JSON-bestand op een toegankelijke locatie voor het implementeren van een met Docker ingedeelde container. Voer vervolgens de volgende opdracht uit om de container te implementeren Geef het pad naar het JSON-bestand (`marathon.json` in dit voorbeeld).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

U kunt ook de Marathon API gebruiken om in implementaties van toepassingen uit of in te schalen. In het vorige voorbeeld hebt u één exemplaar van een toepassing geïmplementeerd. Laten we dit uitschalen naar drie exemplaren van een toepassing. Dit doet u door een JSON-bestand te maken met behulp van de volgende JSON-tekst en dit op een toegankelijke locatie op te slaan.

```json
{ "instances": 3 }
```

Voer de volgende opdracht uit de toepassing te schalen:

> [!NOTE]
> De URI is http://localhost/marathon/v2/apps/ gevolgd door de id van de toepassing die u wilt schalen. Als u het Nginx-voorbeeld gebruikt dat hier wordt besproken, zou de URI http://localhost/marathon/v2/apps/nginx zijn.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Volgende stappen
* [Lees meer over de Mesos HTTP-eindpunten](http://mesos.apache.org/documentation/latest/endpoints/)
* [Lees meer over de Marathon REST API](https://mesosphere.github.io/marathon/docs/rest-api.html)

