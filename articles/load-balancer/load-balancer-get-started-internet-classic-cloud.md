---
title: Een internetgerichte load balancer maken voor Azure Cloud Services | Microsoft Docs
description: Meer informatie over het maken van een internetgerichte load balancer in het klassieke implementatiemodel voor cloudservices
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="00277-103">Aan de slag met het maken van een internetgerichte load balancer voor cloudservices</span><span class="sxs-lookup"><span data-stu-id="00277-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="00277-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="00277-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="00277-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00277-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="00277-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="00277-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="00277-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="00277-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="00277-108">Voordat u met Azure-resources gaat werken, is het belangrijk om te weten dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="00277-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="00277-109">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="00277-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="00277-110">U kunt de documentatie voor verschillende hulpprogramma's bekijken door op de tabbladen boven aan dit artikel te klikken.</span><span class="sxs-lookup"><span data-stu-id="00277-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="00277-111">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="00277-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="00277-112">Hier vindt u [meer informatie over hoe u een internetgerichte load balancer maakt met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="00277-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="00277-113">Cloudservices worden automatisch geconfigureerd met een load balancer en kunnen worden aangepast via het servicemodel.</span><span class="sxs-lookup"><span data-stu-id="00277-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="00277-114">Een load balancer maken met behulp van het servicedefinitiebestand</span><span class="sxs-lookup"><span data-stu-id="00277-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="00277-115">U kunt gebruikmaken van de Azure SDK voor .NET 2.5 om uw cloudservice bij te werken.</span><span class="sxs-lookup"><span data-stu-id="00277-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="00277-116">Instellingen van eindpunten voor cloudservices kunnen worden aangebracht in het bestand [servicedefinition](https://msdn.microsoft.com/library/azure/gg557553.aspx).csdef.</span><span class="sxs-lookup"><span data-stu-id="00277-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="00277-117">In het volgende voorbeeld ziet u hoe het bestand servicedefinition.csdef voor de implementatie van een cloud is geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="00277-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="00277-118">Als u het fragment voor het .csdef-bestand bekijkt dat is gegenereerd via een cloudimplementatie, kunt u zien dat het externe eindpunt is geconfigureerd voor het gebruik van HTTP-poorten op poort 10000, 10001 en 10002.</span><span class="sxs-lookup"><span data-stu-id="00277-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="00277-119">De status van een load balancer voor cloudservices controleren</span><span class="sxs-lookup"><span data-stu-id="00277-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="00277-120">Hier volgt een voorbeeld van een statustest:</span><span class="sxs-lookup"><span data-stu-id="00277-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="00277-121">De load balancer combineert de gegevens van het eindpunt en de gegevens van de test om een URL te maken met de indeling `http://{DIP of VM}:80/Probe.aspx`. Deze kan worden gebruikt om de status van de service op te vragen.</span><span class="sxs-lookup"><span data-stu-id="00277-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="00277-122">De service detecteert periodieke tests van hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="00277-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="00277-123">Dit is de aanvraag voor een statustest die afkomstig is van de host van het knooppunt waarop de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="00277-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="00277-124">Als de service reageert met een HTTP 200-statuscode, gaat de load balancer ervan uit dat de service in orde is.</span><span class="sxs-lookup"><span data-stu-id="00277-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="00277-125">Bij een andere HTTP-statuscode (bijvoorbeeld 503) wordt de virtuele machine direct uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="00277-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="00277-126">De definitie van de test bepaalt ook de frequentie waarmee de test wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="00277-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="00277-127">In ons geval test de load balancer het eindpunt elke 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="00277-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="00277-128">Als er 10 seconden lang geen positief antwoord wordt ontvangen (twee testintervallen), wordt aangenomen dat de test negatief is en wordt de virtuele machine uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="00277-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="00277-129">Als de service is uitgeschakeld en er een positief antwoord wordt ontvangen, wordt de service direct weer in gebruik genomen.</span><span class="sxs-lookup"><span data-stu-id="00277-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="00277-130">Als de status van de service steeds wisselt tussen goed en slecht, kan de load balancer de service tijdelijk uitgeschakeld houden totdat de status gedurende een aantal tests goed blijkt.</span><span class="sxs-lookup"><span data-stu-id="00277-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="00277-131">Controleer het schema van de servicedefinitie voor de [statustest](https://msdn.microsoft.com/library/azure/jj151530.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="00277-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00277-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="00277-132">Next steps</span></span>

[<span data-ttu-id="00277-133">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="00277-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="00277-134">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="00277-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="00277-135">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="00277-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

