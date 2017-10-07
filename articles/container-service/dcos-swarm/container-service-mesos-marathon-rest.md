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
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="c821e-104">DC/OS-containerbeheer via Hallo Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="c821e-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="c821e-105">DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde werkbelastingen terwijl het Hallo onderliggende hardware wordt onttrokken.</span><span class="sxs-lookup"><span data-stu-id="c821e-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="c821e-106">Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt.</span><span class="sxs-lookup"><span data-stu-id="c821e-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="c821e-107">Er zijn frameworks beschikbaar voor veel populaire werkbelastingen, wordt er in dit document helpt u op weg maken en schalen van containerimplementaties met behulp van Hallo Marathon REST API.</span><span class="sxs-lookup"><span data-stu-id="c821e-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c821e-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c821e-108">Prerequisites</span></span>

<span data-ttu-id="c821e-109">Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="c821e-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="c821e-110">U moet ook toohave externe connectiviteit toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="c821e-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="c821e-111">Zie voor meer informatie over deze items Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c821e-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="c821e-112">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="c821e-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="c821e-113">Verbinding maken met tooan Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="c821e-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="c821e-114">Toegang tot Hallo DC/OS-API 's</span><span class="sxs-lookup"><span data-stu-id="c821e-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="c821e-115">Nadat u verbonden toohello Azure Container Service-cluster bent, kunt u via http://localhost: Local-port Hallo DC/OS en gerelateerde REST-API's openen.</span><span class="sxs-lookup"><span data-stu-id="c821e-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="c821e-116">Hallo-voorbeelden in dit document wordt ervan uitgegaan dat u via tunneling op poort 80.</span><span class="sxs-lookup"><span data-stu-id="c821e-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="c821e-117">Bijvoorbeeld, Hallo Marathon-eindpunten op URI's kunnen worden bereikt vanaf `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="c821e-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="c821e-118">Verschillende API's, Zie voor meer informatie op Hallo Hallo Mesosphere-documentatie voor Hallo [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) en de [Chronos API](https://mesos.github.io/chronos/docs/api.html), en de Apache-documentatie voor Hallo [Mesos Scheduler API ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="c821e-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="c821e-119">Informatie verzamelen van DC/OS en Marathon</span><span class="sxs-lookup"><span data-stu-id="c821e-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="c821e-120">Voordat u containers toohello DC/OS-cluster implementeert, verzamelt u wat informatie over Hallo DC/OS-cluster, zoals Hallo namen en status van Hallo DC/OS-agents.</span><span class="sxs-lookup"><span data-stu-id="c821e-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="c821e-121">toodo query dus Hallo `master/slaves` eindpunt Hallo DC/OS REST-API.</span><span class="sxs-lookup"><span data-stu-id="c821e-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="c821e-122">Als alles goed gaat, retourneert Hallo query een lijst van DC/OS-agents en de verschillende eigenschappen voor elk.</span><span class="sxs-lookup"><span data-stu-id="c821e-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="c821e-123">Nu gebruiken Hallo Marathon `/apps` toocheck eindpunt voor de huidige toepassing implementaties toohello DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="c821e-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="c821e-124">Als dit een nieuw cluster is, ziet u een lege matrix voor apps.</span><span class="sxs-lookup"><span data-stu-id="c821e-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="c821e-125">Een met Docker ingedeelde container implementeren</span><span class="sxs-lookup"><span data-stu-id="c821e-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="c821e-126">U kunt Docker ingedeelde containers via Marathon REST API Hallo implementeren met behulp van een JSON-bestand die Hallo bedoeld implementatie beschrijft.</span><span class="sxs-lookup"><span data-stu-id="c821e-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="c821e-127">Hallo implementeert volgende voorbeeld een Nginx-container tooa persoonlijke agent in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c821e-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

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

<span data-ttu-id="c821e-128">Hallo JSON-bestand toodeploy een met Docker ingedeelde container, opslaan in een toegankelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="c821e-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="c821e-129">Vervolgens toodeploy Hallo-container, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c821e-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="c821e-130">Hallo naam opgeven van Hallo JSON-bestand (`marathon.json` in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="c821e-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="c821e-131">Hallo-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="c821e-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="c821e-132">Nu, als u een query Marathon voor toepassingen uitvoert, deze nieuwe toepassing wordt weergegeven in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c821e-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="c821e-133">Hallo-container bereiken</span><span class="sxs-lookup"><span data-stu-id="c821e-133">Reach hello container</span></span>

<span data-ttu-id="c821e-134">U kunt die Nginx wordt uitgevoerd in een container op een van de persoonlijke agents in het cluster Hallo HALLO hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="c821e-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="c821e-135">toofind hello host en poort waarop Hallo container wordt uitgevoerd, doorzoeken Marathon Hallo actieve taken:</span><span class="sxs-lookup"><span data-stu-id="c821e-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="c821e-136">Hallo-waarde van zoeken `host` in Hallo uitvoer (een IP-adres te vergelijkbare`10.32.0.x`), en de waarde van Hallo `ports`.</span><span class="sxs-lookup"><span data-stu-id="c821e-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="c821e-137">Maak nu een SSH terminal-verbinding (niet via een tunnel verbinding) toohello management FQDN-naam van Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="c821e-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="c821e-138">Eenmaal zijn verbonden, zorg Hallo aanvraag te volgen, vervangen door de juiste waarden Hallo van `host` en `ports`:</span><span class="sxs-lookup"><span data-stu-id="c821e-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="c821e-139">Hallo Nginx server-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="c821e-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx van container](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="c821e-141">Uw containers schalen</span><span class="sxs-lookup"><span data-stu-id="c821e-141">Scale your containers</span></span>
<span data-ttu-id="c821e-142">U kunt Hallo Marathon API tooscale out- of schaal gebruiken in implementaties van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c821e-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="c821e-143">In het vorige voorbeeld hello, moet u een exemplaar van een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c821e-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="c821e-144">Schalen we dit uit toothree exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="c821e-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="c821e-145">toodo dus een JSON-bestand maken met behulp van de volgende JSON-tekst hello en sla deze op een toegankelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="c821e-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="c821e-146">Uitvoeren van uw verbinding via een tunnel, Hallo opdracht tooscale uit de toepassing hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="c821e-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="c821e-147">Hallo-URI is http://localhost/marathon/v2/apps/ gevolgd door het Hallo-ID van Hallo toepassing tooscale.</span><span class="sxs-lookup"><span data-stu-id="c821e-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="c821e-148">Als u van Hallo Nginx-voorbeeld gebruikt die is opgegeven hier gebruikmaakt, zou Hallo URI http://localhost/marathon/v2/apps/nginx zijn.</span><span class="sxs-lookup"><span data-stu-id="c821e-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="c821e-149">Voer tenslotte een query Hallo Marathon-eindpunt voor toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c821e-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="c821e-150">U zult zien dat er nu drie Nginx-containers zijn.</span><span class="sxs-lookup"><span data-stu-id="c821e-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="c821e-151">Vergelijkbare PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="c821e-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="c821e-152">U kunt dezelfde acties uitvoeren met behulp van PowerShell-opdrachten in een Windows-systeem.</span><span class="sxs-lookup"><span data-stu-id="c821e-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="c821e-153">toogather informatie over Hallo DC/OS-cluster, zoals agentnamen en agentstatus, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c821e-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="c821e-154">U kunt Docker ingedeelde containers via Marathon implementeren met behulp van een JSON-bestand die Hallo bedoeld implementatie beschrijft.</span><span class="sxs-lookup"><span data-stu-id="c821e-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="c821e-155">Hallo implementeert volgende voorbeeld Hallo Nginx-container, binding van poort 80 van Hallo DC/OS-agent tooport 80 van Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="c821e-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

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

<span data-ttu-id="c821e-156">Hallo JSON-bestand toodeploy een met Docker ingedeelde container, opslaan in een toegankelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="c821e-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="c821e-157">Vervolgens toodeploy Hallo-container, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c821e-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="c821e-158">Geef Hallo pad toohello JSON-bestand (`marathon.json` in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="c821e-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="c821e-159">U kunt ook Hallo Marathon API tooscale out- of schaal gebruiken in implementaties van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c821e-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="c821e-160">In het vorige voorbeeld hello, moet u een exemplaar van een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c821e-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="c821e-161">Schalen we dit uit toothree exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="c821e-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="c821e-162">toodo dus een JSON-bestand maken met behulp van de volgende JSON-tekst hello en sla deze op een toegankelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="c821e-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="c821e-163">Voer Hallo opdracht tooscale uit de toepassing hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c821e-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="c821e-164">Hallo-URI is http://localhost/marathon/v2/apps/ gevolgd door het Hallo-ID van Hallo toepassing tooscale.</span><span class="sxs-lookup"><span data-stu-id="c821e-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="c821e-165">Als u van Hallo Nginx-voorbeeld opgegeven hier gebruikmaakt, zou Hallo URI http://localhost/marathon/v2/apps/nginx zijn.</span><span class="sxs-lookup"><span data-stu-id="c821e-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="c821e-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c821e-166">Next steps</span></span>
* [<span data-ttu-id="c821e-167">Lees meer over Hallo Mesos HTTP-eindpunten</span><span class="sxs-lookup"><span data-stu-id="c821e-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="c821e-168">Lees meer over Hallo Marathon REST API</span><span class="sxs-lookup"><span data-stu-id="c821e-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

