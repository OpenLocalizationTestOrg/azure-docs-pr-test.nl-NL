---
title: aaaManage Azure DC/OS-cluster met Marathon-gebruikersinterface | Microsoft Docs
description: Containers tooan Azure Container Service-cluster-service implementeren met behulp van Hallo webgebruikersinterface van Marathon.
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
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="88d04-104">Een Azure Container Service DC/OS-cluster via Hallo webgebruikersinterface van Marathon beheren</span><span class="sxs-lookup"><span data-stu-id="88d04-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="88d04-105">DC/OS biedt een omgeving voor het implementeren en schalen van geclusterde werkbelastingen terwijl het Hallo onderliggende hardware wordt onttrokken.</span><span class="sxs-lookup"><span data-stu-id="88d04-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="88d04-106">Op de DC/OS ligt een framework dat de planning en uitvoering van rekenworkloads regelt.</span><span class="sxs-lookup"><span data-stu-id="88d04-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="88d04-107">Terwijl frameworks er beschikbaar zijn voor veel populaire werkbelastingen, wordt in dit document beschrijft hoe tooget gestart voor het implementeren van containers met Marathon.</span><span class="sxs-lookup"><span data-stu-id="88d04-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="88d04-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88d04-108">Prerequisites</span></span>
<span data-ttu-id="88d04-109">Voer het uitvoeren van deze voorbeelden hebt u een DC/OS-cluster nodig dat is geconfigureerd in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="88d04-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="88d04-110">U moet ook toohave externe connectiviteit toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="88d04-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="88d04-111">Zie voor meer informatie over deze items Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="88d04-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="88d04-112">Een Azure Container Service-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="88d04-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="88d04-113">Verbinding maken met tooan Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="88d04-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="88d04-114">In dit artikel wordt ervan uitgegaan dat u toohello DC/OS-cluster via tunneling via uw lokale poort 80.</span><span class="sxs-lookup"><span data-stu-id="88d04-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="88d04-115">Hallo DC/OS-gebruikersinterface verkennen</span><span class="sxs-lookup"><span data-stu-id="88d04-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="88d04-116">Met een tunnel Secure Shell (SSH) [tot stand gebracht](../container-service-connect.md), toohttp://localhost/ bladeren.</span><span class="sxs-lookup"><span data-stu-id="88d04-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="88d04-117">Dit wordt Hallo DC/OS-webgebruikersinterface geladen en informatie over het Hallo-cluster, zoals gebruikte resources, actieve agents en actieve services.</span><span class="sxs-lookup"><span data-stu-id="88d04-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![DC/OS-webgebruikersinterface](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="88d04-119">Hallo Marathon-gebruikersinterface verkennen</span><span class="sxs-lookup"><span data-stu-id="88d04-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="88d04-120">toosee hello Marathon-gebruikersinterface toohttp://localhost/marathon bladeren.</span><span class="sxs-lookup"><span data-stu-id="88d04-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="88d04-121">In dit scherm kunt u een nieuwe container of een andere toepassing starten op Hallo Azure Container Service DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="88d04-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="88d04-122">U ziet ook informatie over actieve containers en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="88d04-122">You can also see information about running containers and applications.</span></span>  

![Marathon-gebruikersinterface](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="88d04-124">Een met Docker ingedeelde container implementeren</span><span class="sxs-lookup"><span data-stu-id="88d04-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="88d04-125">toodeploy een nieuwe container via Marathon, klikt u op **toepassing maken**, en voer de volgende informatie in Hallo formuliertabbladen Hallo:</span><span class="sxs-lookup"><span data-stu-id="88d04-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="88d04-126">Veld</span><span class="sxs-lookup"><span data-stu-id="88d04-126">Field</span></span> | <span data-ttu-id="88d04-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="88d04-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="88d04-128">Id</span><span class="sxs-lookup"><span data-stu-id="88d04-128">ID</span></span> |<span data-ttu-id="88d04-129">nginx</span><span class="sxs-lookup"><span data-stu-id="88d04-129">nginx</span></span> |
| <span data-ttu-id="88d04-130">Geheugen</span><span class="sxs-lookup"><span data-stu-id="88d04-130">Memory</span></span> | <span data-ttu-id="88d04-131">32</span><span class="sxs-lookup"><span data-stu-id="88d04-131">32</span></span> |
| <span data-ttu-id="88d04-132">Installatiekopie</span><span class="sxs-lookup"><span data-stu-id="88d04-132">Image</span></span> |<span data-ttu-id="88d04-133">nginx</span><span class="sxs-lookup"><span data-stu-id="88d04-133">nginx</span></span> |
| <span data-ttu-id="88d04-134">Netwerk</span><span class="sxs-lookup"><span data-stu-id="88d04-134">Network</span></span> |<span data-ttu-id="88d04-135">Overbrugd</span><span class="sxs-lookup"><span data-stu-id="88d04-135">Bridged</span></span> |
| <span data-ttu-id="88d04-136">Hostpoort</span><span class="sxs-lookup"><span data-stu-id="88d04-136">Host Port</span></span> |<span data-ttu-id="88d04-137">80</span><span class="sxs-lookup"><span data-stu-id="88d04-137">80</span></span> |
| <span data-ttu-id="88d04-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="88d04-138">Protocol</span></span> |<span data-ttu-id="88d04-139">TCP</span><span class="sxs-lookup"><span data-stu-id="88d04-139">TCP</span></span> |

![Nieuwe toepassingsgebruikersinterface: algemeen](./media/container-service-mesos-marathon-ui/dcos4.png)

![Nieuwe toepassingsgebruikersinterface: Docker-container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Nieuwe toepassingsgebruikersinterface: poort- en servicedetectie](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="88d04-143">Als u wilt dat toostatically kaart Hallo container poort tooa poort op Hallo-agent, moet u toouse JSON-modus.</span><span class="sxs-lookup"><span data-stu-id="88d04-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="88d04-144">Ja, schakelt de wizard nieuwe toepassing hello te toodo**JSON-modus** met behulp van Hallo in-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="88d04-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="88d04-145">Voer vervolgens de volgende instelling onder Hallo Hallo `portMappings` sectie van de definitie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="88d04-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="88d04-146">In het volgende voorbeeld wordt poort 80 van Hallo container tooport 80 Hallo DC/OS-agent.</span><span class="sxs-lookup"><span data-stu-id="88d04-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="88d04-147">Nadat u deze wijziging hebt aangebracht, kunt u deze wizard uit JSON-modus halen.</span><span class="sxs-lookup"><span data-stu-id="88d04-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Nieuwe toepassingsgebruikersinterface: voorbeeld van poort 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="88d04-149">Als u tooenable statuscontroles wilt, stelt u een pad op Hallo **Health controleert** tabblad.</span><span class="sxs-lookup"><span data-stu-id="88d04-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Nieuwe toepassingsgebruikersinterface: statuscontroles](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="88d04-151">Hallo DC/OS-cluster wordt geïmplementeerd met set persoonlijke en openbare agents.</span><span class="sxs-lookup"><span data-stu-id="88d04-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="88d04-152">Hallo cluster toobe kunnen tooaccess toepassingen van Hallo Internet moet u toodeploy Hallo toepassingen tooa openbare agent.</span><span class="sxs-lookup"><span data-stu-id="88d04-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="88d04-153">toodo Selecteer daarom Hallo **optioneel** tabblad van de wizard nieuwe toepassing hello en voer **slave_public** voor Hallo **geaccepteerde resourcerollen**.</span><span class="sxs-lookup"><span data-stu-id="88d04-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="88d04-154">Klik vervolgens op **Toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="88d04-154">Then click **Create Application**.</span></span>

![Nieuwe toepassingsgebruikersinterface: instellingen openbare agent](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="88d04-156">Terug op Hallo hoofdpagina van Marathon ziet u Hallo Implementatiestatus voor Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="88d04-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="88d04-157">Eerst wordt de status **Implementeren** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="88d04-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="88d04-158">Na een geslaagde implementatie Hallo statuswijzigingen te**met**.</span><span class="sxs-lookup"><span data-stu-id="88d04-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Hoofdpagina van Marathon: implementatiestatus van container](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="88d04-160">Wanneer u overschakelt back toohello DC/OS-webgebruikersinterface (http://localhost/), ziet u dat een taak (in dit geval een met Docker ingedeelde container) wordt uitgevoerd op Hallo DC/OS-cluster.</span><span class="sxs-lookup"><span data-stu-id="88d04-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![DC/OS-webgebruikersinterface: taak uitgevoerd op Hallo-cluster](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="88d04-162">toosee hello clusterknooppunt die taak Hallo op wordt uitgevoerd, klikt u op Hallo **knooppunten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="88d04-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![DC/OS-webgebruikersinterface: clusterknooppunt van taak](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="88d04-164">Hallo-container bereiken</span><span class="sxs-lookup"><span data-stu-id="88d04-164">Reach hello container</span></span>

<span data-ttu-id="88d04-165">In dit voorbeeld wordt Hallo toepassing uitgevoerd op een knooppunt openbare agent.</span><span class="sxs-lookup"><span data-stu-id="88d04-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="88d04-166">U bereikt Hallo toepassing hello internet door te bladeren toohello agent FQDN-naam van de cluster Hallo: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, waarbij:</span><span class="sxs-lookup"><span data-stu-id="88d04-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="88d04-167">**DNSPREFIX** Hallo DNS-voorvoegsel op dat u hebt opgegeven tijdens de implementatie Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="88d04-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="88d04-168">**REGIO** Hallo regio waarin uw resourcegroep zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="88d04-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx van Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="88d04-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88d04-170">Next steps</span></span>
* [<span data-ttu-id="88d04-171">Werken met DC/OS en Marathon API Hallo</span><span class="sxs-lookup"><span data-stu-id="88d04-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="88d04-172">Deep dive op Hallo Azure Container Service met Mesos</span><span class="sxs-lookup"><span data-stu-id="88d04-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
