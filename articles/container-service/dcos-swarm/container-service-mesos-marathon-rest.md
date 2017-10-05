---
title: Beheren van Azure DC/OS-cluster met Marathon REST API | Microsoft Docs
description: Implementeer containers naar een Azure Container Service DC/OS-cluster met behulp van de Marathon REST API.
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
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="d1d71-104">DC/OS-containerbeheer via de Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="d1d71-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="d1d71-105">DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde workloads terwijl de onderliggende hardware wordt onttrokken.</span><span class="sxs-lookup"><span data-stu-id="d1d71-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="d1d71-106">Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt.</span><span class="sxs-lookup"><span data-stu-id="d1d71-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="d1d71-107">Er zijn frameworks beschikbaar voor veel populaire werkbelastingen, wordt er in dit document helpt u op weg maken en schalen van containerimplementaties met behulp van de Marathon REST API.</span><span class="sxs-lookup"><span data-stu-id="d1d71-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d1d71-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d1d71-108">Prerequisites</span></span>

<span data-ttu-id="d1d71-109">Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="d1d71-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="d1d71-110">U hebt ook een externe verbinding met dit cluster nodig.</span><span class="sxs-lookup"><span data-stu-id="d1d71-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="d1d71-111">Zie de volgende artikelen voor meer informatie over deze items:</span><span class="sxs-lookup"><span data-stu-id="d1d71-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="d1d71-112">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="d1d71-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="d1d71-113">Verbinding maken met een Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="d1d71-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="d1d71-114">Toegang tot de DC/OS-API 's</span><span class="sxs-lookup"><span data-stu-id="d1d71-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="d1d71-115">Nadat u met het Azure Container Service-cluster bent verbonden, hebt u via http://localhost:local-port toegang tot DC/OS en gerelateerde REST API's.</span><span class="sxs-lookup"><span data-stu-id="d1d71-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="d1d71-116">In de voorbeelden in dit document wordt ervan uitgegaan dat u poort 80 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d1d71-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="d1d71-117">Bijvoorbeeld, de Marathon-eindpunten op URI's kunnen worden bereikt vanaf `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="d1d71-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="d1d71-118">Zie voor meer informatie over de verschillende API's de Mesosphere-documentatie voor de [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) en de [Chronos API](https://mesos.github.io/chronos/docs/api.html), en de Apache-documentatie voor de [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="d1d71-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="d1d71-119">Informatie verzamelen van DC/OS en Marathon</span><span class="sxs-lookup"><span data-stu-id="d1d71-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="d1d71-120">Voordat u containers naar het DC/OS-cluster implementeert, verzamelt u wat informatie over het DC/OS-cluster, zoals de namen en de status van de DC/OS-agents.</span><span class="sxs-lookup"><span data-stu-id="d1d71-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="d1d71-121">U doet dit door een query uit te voeren op het `master/slaves`-eindpunt van de DC/OS REST API.</span><span class="sxs-lookup"><span data-stu-id="d1d71-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="d1d71-122">Als alles goed gaat, wordt met de query een lijst geretourneerd van DC/OS-agents en de verschillende eigenschappen voor elke agent.</span><span class="sxs-lookup"><span data-stu-id="d1d71-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="d1d71-123">Gebruik nu het Marathon `/apps`-eindpunt om te controleren op huidige implementaties naar het DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d71-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="d1d71-124">Als dit een nieuw cluster is, ziet u een lege matrix voor apps.</span><span class="sxs-lookup"><span data-stu-id="d1d71-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="d1d71-125">Een met Docker ingedeelde container implementeren</span><span class="sxs-lookup"><span data-stu-id="d1d71-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="d1d71-126">U kunt Docker ingedeelde containers via Marathon REST-API implementeren met behulp van een JSON-bestand dat het doel van de implementatie beschrijft.</span><span class="sxs-lookup"><span data-stu-id="d1d71-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="d1d71-127">Het volgende voorbeeld wordt een Nginx-container geïmplementeerd naar een persoonlijke agent in het cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d71-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

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

<span data-ttu-id="d1d71-128">Sla het JSON-bestand op een toegankelijke locatie voor het implementeren van een met Docker ingedeelde container.</span><span class="sxs-lookup"><span data-stu-id="d1d71-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="d1d71-129">Voer vervolgens de volgende opdracht uit om de container te implementeren</span><span class="sxs-lookup"><span data-stu-id="d1d71-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="d1d71-130">Geef de naam van het JSON-bestand (`marathon.json` in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="d1d71-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="d1d71-131">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="d1d71-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="d1d71-132">Als u in Marathon toepassingen opvraagt via een query, wordt deze nieuwe toepassing in de uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d1d71-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="d1d71-133">De container bereiken</span><span class="sxs-lookup"><span data-stu-id="d1d71-133">Reach the container</span></span>

<span data-ttu-id="d1d71-134">U kunt controleren of de Nginx wordt uitgevoerd in een container op een van de persoonlijke agents in het cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d71-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="d1d71-135">Als u wilt zoeken op de host en de poort waarop de container wordt uitgevoerd, query Marathon voor actieve taken:</span><span class="sxs-lookup"><span data-stu-id="d1d71-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="d1d71-136">De waarde van zoeken `host` in de uitvoer (een IP-adres dat lijkt op `10.32.0.x`), en de waarde van `ports`.</span><span class="sxs-lookup"><span data-stu-id="d1d71-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="d1d71-137">Nu een terminal SSH-verbinding (niet via een tunnel verbinding) aanbrengen in de management FQDN-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d71-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="d1d71-138">Eenmaal zijn verbonden, maken de volgende aanvraag, vervangen door de juiste waarden van `host` en `ports`:</span><span class="sxs-lookup"><span data-stu-id="d1d71-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="d1d71-139">De uitvoer van de server Nginx is vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="d1d71-139">The Nginx server output is similar to the following:</span></span>

![Nginx van container](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="d1d71-141">Uw containers schalen</span><span class="sxs-lookup"><span data-stu-id="d1d71-141">Scale your containers</span></span>
<span data-ttu-id="d1d71-142">U kunt de Marathon API uitbreiden of schalen in implementaties van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d1d71-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="d1d71-143">In het vorige voorbeeld hebt u één exemplaar van een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d1d71-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d1d71-144">Laten we dit uitschalen naar drie exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1d71-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="d1d71-145">Dit doet u door een JSON-bestand te maken met behulp van de volgende JSON-tekst en dit op een toegankelijke locatie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d1d71-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d1d71-146">Voer de volgende opdracht uit de toepassing te schalen van uw via een tunnel verbinding.</span><span class="sxs-lookup"><span data-stu-id="d1d71-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="d1d71-147">De URI is http://localhost/marathon/v2/apps/ gevolgd door de id van de toepassing die u wilt schalen.</span><span class="sxs-lookup"><span data-stu-id="d1d71-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="d1d71-148">Als u het Nginx-voorbeeld gebruikt dat hier wordt besproken, zou de URI http://localhost/marathon/v2/apps/nginx zijn.</span><span class="sxs-lookup"><span data-stu-id="d1d71-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="d1d71-149">Voer tenslotte een query voor toepassingen uit op het Marathon-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d1d71-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="d1d71-150">U zult zien dat er nu drie Nginx-containers zijn.</span><span class="sxs-lookup"><span data-stu-id="d1d71-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="d1d71-151">Vergelijkbare PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="d1d71-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="d1d71-152">U kunt dezelfde acties uitvoeren met behulp van PowerShell-opdrachten in een Windows-systeem.</span><span class="sxs-lookup"><span data-stu-id="d1d71-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="d1d71-153">Voor het verzamelen van informatie over het DC/OS-cluster, zoals agentnamen en agentstatus, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d1d71-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="d1d71-154">U implementeert met Docker ingedeelde containers via Marathon met behulp van een JSON-bestand waarin het doel van de implementatie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d1d71-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="d1d71-155">In het volgende voorbeeld wordt de Nginx-container geïmplementeerd, met een binding van poort 80 van de DC/OS-agent naar poort 80 van de container.</span><span class="sxs-lookup"><span data-stu-id="d1d71-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

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

<span data-ttu-id="d1d71-156">Sla het JSON-bestand op een toegankelijke locatie voor het implementeren van een met Docker ingedeelde container.</span><span class="sxs-lookup"><span data-stu-id="d1d71-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="d1d71-157">Voer vervolgens de volgende opdracht uit om de container te implementeren</span><span class="sxs-lookup"><span data-stu-id="d1d71-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="d1d71-158">Geef het pad naar het JSON-bestand (`marathon.json` in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="d1d71-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="d1d71-159">U kunt ook de Marathon API gebruiken om in implementaties van toepassingen uit of in te schalen.</span><span class="sxs-lookup"><span data-stu-id="d1d71-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="d1d71-160">In het vorige voorbeeld hebt u één exemplaar van een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d1d71-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d1d71-161">Laten we dit uitschalen naar drie exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1d71-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="d1d71-162">Dit doet u door een JSON-bestand te maken met behulp van de volgende JSON-tekst en dit op een toegankelijke locatie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d1d71-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d1d71-163">Voer de volgende opdracht uit de toepassing te schalen:</span><span class="sxs-lookup"><span data-stu-id="d1d71-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="d1d71-164">De URI is http://localhost/marathon/v2/apps/ gevolgd door de id van de toepassing die u wilt schalen.</span><span class="sxs-lookup"><span data-stu-id="d1d71-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="d1d71-165">Als u het Nginx-voorbeeld gebruikt dat hier wordt besproken, zou de URI http://localhost/marathon/v2/apps/nginx zijn.</span><span class="sxs-lookup"><span data-stu-id="d1d71-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="d1d71-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1d71-166">Next steps</span></span>
* [<span data-ttu-id="d1d71-167">Lees meer over de Mesos HTTP-eindpunten</span><span class="sxs-lookup"><span data-stu-id="d1d71-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="d1d71-168">Lees meer over de Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="d1d71-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

