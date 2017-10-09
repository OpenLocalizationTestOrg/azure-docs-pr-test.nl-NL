---
title: aaaCreate een internetgerichte load balancer voor Azure-cloudservices | Microsoft Docs
description: Meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler in het klassieke implementatiemodel voor cloudservices
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
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="1d6e2-103">Aan de slag met het maken van een internetgerichte load balancer voor cloudservices</span><span class="sxs-lookup"><span data-stu-id="1d6e2-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d6e2-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1d6e2-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="1d6e2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6e2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="1d6e2-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1d6e2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="1d6e2-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="1d6e2-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="1d6e2-108">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1d6e2-109">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="1d6e2-110">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="1d6e2-111">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="1d6e2-112">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1d6e2-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="1d6e2-113">Cloud-services worden automatisch geconfigureerd met een load balancer en kunnen worden aangepast via Hallo-ServiceModel.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="1d6e2-114">Een load balancer met behulp van het servicedefinitiebestand Hallo maken</span><span class="sxs-lookup"><span data-stu-id="1d6e2-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="1d6e2-115">U kunt hello Azure SDK voor .NET 2.5 tooupdate gebruikmaken van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="1d6e2-116">Instellingen voor endpoint voor cloudservices zijn aangebracht in Hallo [definitie](https://msdn.microsoft.com/library/azure/gg557553.aspx) csdef-bestand.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="1d6e2-117">Hallo volgende voorbeeld laat zien hoe een servicedefinition.csdef-bestand voor de implementatie van een cloud is geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="1d6e2-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="1d6e2-118">Hallo codefragment voor Hallo csdef-bestand is gegenereerd door de implementatie van een cloud te controleren, kunt u Hallo Extern eindpunt geconfigureerd toouse poorten HTTP op poort 10000, 10001 en 10002 zien.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="1d6e2-119">De status van een load balancer voor cloudservices controleren</span><span class="sxs-lookup"><span data-stu-id="1d6e2-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="1d6e2-120">Hallo Hieronder volgt een voorbeeld van een health test:</span><span class="sxs-lookup"><span data-stu-id="1d6e2-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="1d6e2-121">Hallo load balancer combineert Hallo van Hallo eindpunt en Hallo informatie van Hallo test toocreate een URL in de vorm van Hallo `http://{DIP of VM}:80/Probe.aspx` die kunnen worden gebruikt tooquery Hallo status van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="1d6e2-122">Hallo service detecteert periodieke tests uit Hallo hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="1d6e2-123">Dit is Hallo health test aanvraag afkomstig is van de host van knooppunt Hallo Hallo waarop Hallo virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="1d6e2-124">Hallo-service heeft toorespond met een HTTP 200-statuscode voor Hallo load balancer tooassume Hallo-service is in orde.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="1d6e2-125">Andere HTTP-status code (bijvoorbeeld 503) rechtstreeks vergt Hallo virtuele machine uit de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="1d6e2-126">Hallo test definitie bepaalt ook Hallo frequentie van Hallo test.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="1d6e2-127">In ons geval is Hallo load balancer scannen Hallo eindpunt elke 5 seconden.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="1d6e2-128">Als er geen positief antwoord wordt ontvangen voor 10 sec (twee test-intervallen), Hallo test wordt aangenomen dat omlaag en Hallo virtuele machine wordt uitgevoerd buiten de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="1d6e2-129">Op dezelfde manier als Hallo service buiten het wisselen valt en een positief antwoord wordt ontvangen, Hallo service geplaatst terug toorotation meteen.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="1d6e2-130">Als het Hallo-service tussen in orde en slecht veranderen is, besluiten Hallo load balancer toodelay Hallo binnengebracht van Hallo service back toorotation totdat deze is in orde voor een aantal tests.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="1d6e2-131">Controleer Hallo service definitie schema voor Hallo [health test](https://msdn.microsoft.com/library/azure/jj151530.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1d6e2-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d6e2-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d6e2-132">Next steps</span></span>

[<span data-ttu-id="1d6e2-133">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="1d6e2-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="1d6e2-134">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="1d6e2-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1d6e2-135">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="1d6e2-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

