---
title: aaaEnable access tooAzure DC/OS-container app | Microsoft Docs
description: Hoe tooenable openbare toegang krijgen tot tooDC/OS-containers in Azure Container Service.
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="b22ac-104">Openbare toegang tooan Azure Container Service-toepassing inschakelen</span><span class="sxs-lookup"><span data-stu-id="b22ac-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="b22ac-105">Elke DC/OS-container in Hallo ACS [openbare agent groep](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatisch blootgestelde toohello internet.</span><span class="sxs-lookup"><span data-stu-id="b22ac-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="b22ac-106">Standaard-poorten **80**, **443**, **8080** zijn geopend en luistert op deze poorten (openbare) containers toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="b22ac-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="b22ac-107">Dit artikel laat zien hoe tooopen meer poorten voor uw toepassingen in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b22ac-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="b22ac-108">Open een poort (portal)</span><span class="sxs-lookup"><span data-stu-id="b22ac-108">Open a port (portal)</span></span>
<span data-ttu-id="b22ac-109">We moeten eerst tooopen Hallo poort die we willen.</span><span class="sxs-lookup"><span data-stu-id="b22ac-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="b22ac-110">Meld u bij toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="b22ac-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="b22ac-111">Zoeken naar Hallo resourcegroep die u hebt geïmplementeerd hello Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b22ac-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="b22ac-112">Hallo agent load balancer selecteren (die de naam vergelijkbaar te**XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="b22ac-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure container service load balancer](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="b22ac-114">Klik op **Probes** en vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure container service load balancer-tests](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="b22ac-116">Hallo test formulier invullen en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="b22ac-117">Veld</span><span class="sxs-lookup"><span data-stu-id="b22ac-117">Field</span></span> | <span data-ttu-id="b22ac-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b22ac-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b22ac-119">Naam</span><span class="sxs-lookup"><span data-stu-id="b22ac-119">Name</span></span> |<span data-ttu-id="b22ac-120">Een beschrijvende naam van het Hallo-test.</span><span class="sxs-lookup"><span data-stu-id="b22ac-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="b22ac-121">Poort</span><span class="sxs-lookup"><span data-stu-id="b22ac-121">Port</span></span> |<span data-ttu-id="b22ac-122">Hallo-poort van Hallo container tootest.</span><span class="sxs-lookup"><span data-stu-id="b22ac-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="b22ac-123">Pad</span><span class="sxs-lookup"><span data-stu-id="b22ac-123">Path</span></span> |<span data-ttu-id="b22ac-124">(Wanneer in de HTTP-modus) Hallo website relatieve pad tooprobe.</span><span class="sxs-lookup"><span data-stu-id="b22ac-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="b22ac-125">HTTPS wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b22ac-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="b22ac-126">Interval</span><span class="sxs-lookup"><span data-stu-id="b22ac-126">Interval</span></span> |<span data-ttu-id="b22ac-127">Hallo hoeveelheid tijd tussen test probeert, in seconden.</span><span class="sxs-lookup"><span data-stu-id="b22ac-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="b22ac-128">Drempelwaarde voor onjuiste status</span><span class="sxs-lookup"><span data-stu-id="b22ac-128">Unhealthy threshold</span></span> |<span data-ttu-id="b22ac-129">Het aantal opeenvolgende test probeert voordat Hallo container niet in orde.</span><span class="sxs-lookup"><span data-stu-id="b22ac-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="b22ac-130">Terug op het Hallo-eigenschappen van Hallo agent load balancer, klikt u op **Taakverdelingsregels** en vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure container service load balancer-regels](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="b22ac-132">Hallo load balancer formulier invullen en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="b22ac-133">Veld</span><span class="sxs-lookup"><span data-stu-id="b22ac-133">Field</span></span> | <span data-ttu-id="b22ac-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b22ac-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b22ac-135">Naam</span><span class="sxs-lookup"><span data-stu-id="b22ac-135">Name</span></span> |<span data-ttu-id="b22ac-136">Een beschrijvende naam Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b22ac-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="b22ac-137">Poort</span><span class="sxs-lookup"><span data-stu-id="b22ac-137">Port</span></span> |<span data-ttu-id="b22ac-138">Hallo openbare binnenkomende poort.</span><span class="sxs-lookup"><span data-stu-id="b22ac-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="b22ac-139">Back-endpoort</span><span class="sxs-lookup"><span data-stu-id="b22ac-139">Backend port</span></span> |<span data-ttu-id="b22ac-140">Hallo interne openbare poort van Hallo container tooroute verkeer naar.</span><span class="sxs-lookup"><span data-stu-id="b22ac-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="b22ac-141">Back-endpool</span><span class="sxs-lookup"><span data-stu-id="b22ac-141">Backend pool</span></span> |<span data-ttu-id="b22ac-142">Hallo-containers in deze groep worden Hallo doel voor deze load balancer.</span><span class="sxs-lookup"><span data-stu-id="b22ac-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="b22ac-143">Test</span><span class="sxs-lookup"><span data-stu-id="b22ac-143">Probe</span></span> |<span data-ttu-id="b22ac-144">Hallo toodetermine test die wordt gebruikt als een doel in Hallo **back-endpool** in orde is.</span><span class="sxs-lookup"><span data-stu-id="b22ac-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="b22ac-145">Sessiepersistentie</span><span class="sxs-lookup"><span data-stu-id="b22ac-145">Session persistence</span></span> |<span data-ttu-id="b22ac-146">Hiermee wordt bepaald hoe het verkeer van een client voor Hallo duur van Hallo sessie moet worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b22ac-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="b22ac-147">**Geen**: opeenvolgende aanvragen van Hallo dezelfde client door elke container kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b22ac-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="b22ac-148">**Client IP**: opeenvolgende aanvragen van hetzelfde client-IP-worden afgehandeld door Hallo Hallo dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="b22ac-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="b22ac-149">**Client IP en -protocol**: opeenvolgende aanvragen van dezelfde combinatie van client en het IP-protocol worden afgehandeld door Hallo Hallo dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="b22ac-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="b22ac-150">Time-out voor inactiviteit</span><span class="sxs-lookup"><span data-stu-id="b22ac-150">Idle timeout</span></span> |<span data-ttu-id="b22ac-151">(Alleen TCP) Hallo in minuten, tijd tookeep een TCP/HTTP-client openen zonder afhankelijk te zijn van *keepalive-* berichten.</span><span class="sxs-lookup"><span data-stu-id="b22ac-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="b22ac-152">Toevoegen van een beveiligingsregel (portal)</span><span class="sxs-lookup"><span data-stu-id="b22ac-152">Add a security rule (portal)</span></span>
<span data-ttu-id="b22ac-153">Vervolgens moet een regel waarmee verkeer van onze poort is geopend via de firewall Hallo tooadd.</span><span class="sxs-lookup"><span data-stu-id="b22ac-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="b22ac-154">Meld u bij toohello-portal.</span><span class="sxs-lookup"><span data-stu-id="b22ac-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="b22ac-155">Zoeken naar Hallo resourcegroep die u hebt geïmplementeerd hello Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="b22ac-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="b22ac-156">Selecteer Hallo **openbare** netwerkbeveiligingsgroep agent (die de naam vergelijkbaar te**XXXX-agent-openbare-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="b22ac-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure container service-netwerkbeveiligingsgroep](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="b22ac-158">Selecteer **inkomende beveiligingsregels** en vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure container service netwerkbeveiligingsgroepen](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="b22ac-160">Hallo firewall regel tooallow vullen met de openbare poort en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="b22ac-161">Veld</span><span class="sxs-lookup"><span data-stu-id="b22ac-161">Field</span></span> | <span data-ttu-id="b22ac-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b22ac-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b22ac-163">Naam</span><span class="sxs-lookup"><span data-stu-id="b22ac-163">Name</span></span> |<span data-ttu-id="b22ac-164">Een beschrijvende naam van de firewallregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b22ac-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="b22ac-165">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="b22ac-165">Priority</span></span> |<span data-ttu-id="b22ac-166">De positie van de prioriteit voor Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="b22ac-166">Priority rank for hello rule.</span></span> <span data-ttu-id="b22ac-167">Hallo lagere Hallo nummer Hallo hogere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="b22ac-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="b22ac-168">Bron</span><span class="sxs-lookup"><span data-stu-id="b22ac-168">Source</span></span> |<span data-ttu-id="b22ac-169">Hallo binnenkomende IP-adresbereik toobe toegestaan of geweigerd door deze regel beperken.</span><span class="sxs-lookup"><span data-stu-id="b22ac-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="b22ac-170">Gebruik **eventuele** toonot beperking opgeven.</span><span class="sxs-lookup"><span data-stu-id="b22ac-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="b22ac-171">Service</span><span class="sxs-lookup"><span data-stu-id="b22ac-171">Service</span></span> |<span data-ttu-id="b22ac-172">Selecteer een set vooraf gedefinieerde services is bedoeld voor deze regel.</span><span class="sxs-lookup"><span data-stu-id="b22ac-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="b22ac-173">Gebruik anders **aangepaste** toocreate zelf.</span><span class="sxs-lookup"><span data-stu-id="b22ac-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="b22ac-174">Protocol</span><span class="sxs-lookup"><span data-stu-id="b22ac-174">Protocol</span></span> |<span data-ttu-id="b22ac-175">Op basis van verkeer te beperken **TCP** of **UDP**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="b22ac-176">Gebruik **eventuele** toonot beperking opgeven.</span><span class="sxs-lookup"><span data-stu-id="b22ac-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="b22ac-177">Poortbereik</span><span class="sxs-lookup"><span data-stu-id="b22ac-177">Port range</span></span> |<span data-ttu-id="b22ac-178">Wanneer **Service** is **aangepaste**, bepaalt Hallo bereik van de poorten die door deze regel is van invloed op.</span><span class="sxs-lookup"><span data-stu-id="b22ac-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="b22ac-179">U kunt een losse poort zijn, zoals **80**, of een bereik, zoals **1024 1500**.</span><span class="sxs-lookup"><span data-stu-id="b22ac-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="b22ac-180">Actie</span><span class="sxs-lookup"><span data-stu-id="b22ac-180">Action</span></span> |<span data-ttu-id="b22ac-181">Verkeer toestaan of weigeren die voldoen aan de criteria Hallo.</span><span class="sxs-lookup"><span data-stu-id="b22ac-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b22ac-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b22ac-182">Next steps</span></span>
<span data-ttu-id="b22ac-183">Meer informatie over het verschil tussen Hallo [openbare en persoonlijke DC/OS-agents](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="b22ac-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="b22ac-184">Meer informatie lezen over [beheer van uw DC/OS-containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="b22ac-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

