---
title: Beheren van Azure DC/OS-cluster met Marathon-gebruikersinterface | Microsoft Docs
description: Implementeer containers naar een Azure Container Service-cluster met behulp van de webgebruikersinterface van Marathon.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: b00088bb005519dc5d533433308c0e3e33c7f433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="542e9-104">Een DC/OS-cluster in Azure Container Service beheren via de webgebruikersinterface van Marathon</span><span class="sxs-lookup"><span data-stu-id="542e9-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="542e9-105">DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde workloads terwijl de onderliggende hardware wordt onttrokken.</span><span class="sxs-lookup"><span data-stu-id="542e9-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="542e9-106">Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt.</span><span class="sxs-lookup"><span data-stu-id="542e9-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="542e9-107">Terwijl frameworks er beschikbaar zijn voor veel populaire workloads, geeft dit document wordt beschreven hoe om te beginnen met het implementeren van containers met Marathon.</span><span class="sxs-lookup"><span data-stu-id="542e9-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="542e9-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="542e9-108">Prerequisites</span></span>
<span data-ttu-id="542e9-109">Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="542e9-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="542e9-110">U hebt ook een externe verbinding met dit cluster nodig.</span><span class="sxs-lookup"><span data-stu-id="542e9-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="542e9-111">Zie de volgende artikelen voor meer informatie over deze items:</span><span class="sxs-lookup"><span data-stu-id="542e9-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="542e9-112">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="542e9-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="542e9-113">Verbinding maken met een Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="542e9-113">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="542e9-114">In dit artikel wordt ervan uitgegaan dat u naar het DC/OS-cluster zijn tunneling via uw lokale poort 80.</span><span class="sxs-lookup"><span data-stu-id="542e9-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="542e9-115">De DC/OS-gebruikersinterface verkennen</span><span class="sxs-lookup"><span data-stu-id="542e9-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="542e9-116">Wanneer een SSH-tunnel (Secure Shell) is [ingesteld](../container-service-connect.md), gaat u naar http://localhost/.</span><span class="sxs-lookup"><span data-stu-id="542e9-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="542e9-117">Hierdoor wordt de DC/OS-webgebruikersinterface geladen met informatie over het cluster, zoals gebruikte resources, actieve agents en actieve services.</span><span class="sxs-lookup"><span data-stu-id="542e9-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS-webgebruikersinterface](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="542e9-119">De Marathon-gebruikersinterface verkennen</span><span class="sxs-lookup"><span data-stu-id="542e9-119">Explore the Marathon UI</span></span>
<span data-ttu-id="542e9-120">Ga naar http://localhost/marathon overzicht van de Marathon-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="542e9-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="542e9-121">In dit scherm kunt u een nieuwe container of een andere toepassing starten op het DC/OS-cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="542e9-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="542e9-122">U ziet ook informatie over actieve containers en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="542e9-122">You can also see information about running containers and applications.</span></span>  

![Marathon-gebruikersinterface](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="542e9-124">Een met Docker ingedeelde container implementeren</span><span class="sxs-lookup"><span data-stu-id="542e9-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="542e9-125">Voor het implementeren van een nieuwe container via Marathon, klikt u op **Toepassing maken** en voert u de volgende gegevens op de tabbladen van het formulier in:</span><span class="sxs-lookup"><span data-stu-id="542e9-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="542e9-126">Veld</span><span class="sxs-lookup"><span data-stu-id="542e9-126">Field</span></span> | <span data-ttu-id="542e9-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="542e9-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="542e9-128">Id</span><span class="sxs-lookup"><span data-stu-id="542e9-128">ID</span></span> |<span data-ttu-id="542e9-129">nginx</span><span class="sxs-lookup"><span data-stu-id="542e9-129">nginx</span></span> |
| <span data-ttu-id="542e9-130">Geheugen</span><span class="sxs-lookup"><span data-stu-id="542e9-130">Memory</span></span> | <span data-ttu-id="542e9-131">32</span><span class="sxs-lookup"><span data-stu-id="542e9-131">32</span></span> |
| <span data-ttu-id="542e9-132">Installatiekopie</span><span class="sxs-lookup"><span data-stu-id="542e9-132">Image</span></span> |<span data-ttu-id="542e9-133">nginx</span><span class="sxs-lookup"><span data-stu-id="542e9-133">nginx</span></span> |
| <span data-ttu-id="542e9-134">Netwerk</span><span class="sxs-lookup"><span data-stu-id="542e9-134">Network</span></span> |<span data-ttu-id="542e9-135">Overbrugd</span><span class="sxs-lookup"><span data-stu-id="542e9-135">Bridged</span></span> |
| <span data-ttu-id="542e9-136">Hostpoort</span><span class="sxs-lookup"><span data-stu-id="542e9-136">Host Port</span></span> |<span data-ttu-id="542e9-137">80</span><span class="sxs-lookup"><span data-stu-id="542e9-137">80</span></span> |
| <span data-ttu-id="542e9-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="542e9-138">Protocol</span></span> |<span data-ttu-id="542e9-139">TCP</span><span class="sxs-lookup"><span data-stu-id="542e9-139">TCP</span></span> |

![Nieuwe toepassingsgebruikersinterface: algemeen](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nieuwe toepassingsgebruikersinterface: Docker-container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nieuwe toepassingsgebruikersinterface: poort- en servicedetectie](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="542e9-143">Als u de containerpoort statisch wilt toewijzen aan een poort op de agent, gebruikt u de JSON-modus.</span><span class="sxs-lookup"><span data-stu-id="542e9-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="542e9-144">U doet dit door de wizard Nieuwe toepassing over te schakelen naar de **JSON-modus** met behulp van de wisselknop.</span><span class="sxs-lookup"><span data-stu-id="542e9-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="542e9-145">Voer daarna de volgende instelling in onder de sectie `portMappings` van de definitie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="542e9-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="542e9-146">In dit voorbeeld wordt poort 80 van de container gebonden aan poort 80 van de DC/OS-agent.</span><span class="sxs-lookup"><span data-stu-id="542e9-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="542e9-147">Nadat u deze wijziging hebt aangebracht, kunt u deze wizard uit JSON-modus halen.</span><span class="sxs-lookup"><span data-stu-id="542e9-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Nieuwe toepassingsgebruikersinterface: voorbeeld van poort 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="542e9-149">Als u statuscontroles wilt inschakelen, stelt u een pad in op het tabblad **Statuscontroles**.</span><span class="sxs-lookup"><span data-stu-id="542e9-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![Nieuwe toepassingsgebruikersinterface: statuscontroles](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="542e9-151">Het DC/OS-cluster wordt geïmplementeerd met een set persoonlijke en openbare agents.</span><span class="sxs-lookup"><span data-stu-id="542e9-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="542e9-152">Om te zorgen dat het cluster toegang heeft tot toepassingen vanaf internet, moet u de toepassingen implementeren naar een openbare agent.</span><span class="sxs-lookup"><span data-stu-id="542e9-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="542e9-153">Hiertoe selecteert u het tabblad **Optioneel** van de wizard Nieuwe toepassing en voert u **slave_public** in bij de **Geaccepteerde resourcerollen**.</span><span class="sxs-lookup"><span data-stu-id="542e9-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="542e9-154">Klik vervolgens op **Toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="542e9-154">Then click **Create Application**.</span></span>

![Nieuwe toepassingsgebruikersinterface: instellingen openbare agent](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="542e9-156">Op de hoofdpagina van Marathon ziet u de implementatiestatus voor de container.</span><span class="sxs-lookup"><span data-stu-id="542e9-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="542e9-157">Eerst wordt de status **Implementeren** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="542e9-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="542e9-158">Wanneer de implementatie is voltooid, verandert de status in **Uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="542e9-158">After a successful deployment, the status changes to **Running**.</span></span>

![Hoofdpagina van Marathon: implementatiestatus van container](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="542e9-160">Als u terugschakelt naar de DC/OS-webgebruikersinterface (http://localhost/), ziet u dat een taak (in dit geval een container in Docker-indeling) wordt uitgevoerd op het DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="542e9-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![DC/OS-webgebruikersinterface: taak die wordt uitgevoerd op het cluster](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="542e9-162">U kunt het clusterknooppunt waarop de taak wordt uitgevoerd weergeven door op het tabblad **Knooppunten** te klikken.</span><span class="sxs-lookup"><span data-stu-id="542e9-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![DC/OS-webgebruikersinterface: clusterknooppunt van taak](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="542e9-164">De container bereiken</span><span class="sxs-lookup"><span data-stu-id="542e9-164">Reach the container</span></span>

<span data-ttu-id="542e9-165">In dit voorbeeld wordt wordt de toepassing uitgevoerd op een knooppunt openbare agent.</span><span class="sxs-lookup"><span data-stu-id="542e9-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="542e9-166">U bereikt de toepassing van het internet door te bladeren naar de agent FQDN-naam van het cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, waarbij:</span><span class="sxs-lookup"><span data-stu-id="542e9-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="542e9-167">**DNSPREFIX** het DNS-voorvoegsel is dat is opgegeven tijdens de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="542e9-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="542e9-168">**REGION** de regio is waarin uw resourcegroep zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="542e9-168">**REGION** is the region in which your resource group is located.</span></span>

    ![Nginx van Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="542e9-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="542e9-170">Next steps</span></span>
* [<span data-ttu-id="542e9-171">Werken met DC/OS en de Marathon API</span><span class="sxs-lookup"><span data-stu-id="542e9-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="542e9-172">Gedetailleerde uitleg over Azure Container Service met Mesos</span><span class="sxs-lookup"><span data-stu-id="542e9-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
