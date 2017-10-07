---
title: Service Fabric-DNS-service aaaAzure | Microsoft Docs
description: Service Fabric van DNS-service voor het detecteren van microservices van gebruiken in Hallo-cluster.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="8224e-103">DNS-Service in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8224e-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="8224e-104">Hallo DNS-Service is een optionele systeemservice die u in uw cluster toodiscover inschakelen kunt andere services Hallo DNS-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8224e-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="8224e-105">Veel services, vooral beperkte services, een bestaande URL-naam en wordt kunnen tooresolve hebben ze wenselijk, met name in 'lift- en verschuiven'-scenario's voor het gebruik van Hallo standaard DNS-protocol (in plaats van Hallo Naming Service protocol) is.</span><span class="sxs-lookup"><span data-stu-id="8224e-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="8224e-106">Hallo DNS-service kunt u toomap DNS-namen tooa servicenaam en daarom los eindpunt IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="8224e-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="8224e-107">Hallo DNS-service wijst DNS-namen tooservice namen, die op zijn beurt worden opgelost door Hallo Naming Service tooreturn Hallo service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8224e-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="8224e-108">Hallo DNS-naam voor het Hallo-service is opgegeven op Hallo moment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8224e-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Service-eindpunten][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="8224e-110">Hallo DNS-service inschakelen</span><span class="sxs-lookup"><span data-stu-id="8224e-110">Enabling hello DNS service</span></span>
<span data-ttu-id="8224e-111">U moet eerst tooenable Hallo DNS-service in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="8224e-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="8224e-112">Hallo sjabloon ophalen voor Hallo-cluster dat u wilt dat toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8224e-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="8224e-113">U kunt beide Hallo gebruik [voorbeeldsjablonen](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) of een Resource Manager-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="8224e-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="8224e-114">U kunt Hallo DNS-service inschakelen met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8224e-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="8224e-115">Controleer dat Hallo `apiversion` te is ingesteld,`2017-07-01-preview` voor Hallo `Microsoft.ServiceFabric/clusters` resource, en als dat niet bijwerken zoals weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="8224e-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="8224e-116">Nu Hallo DNS-service inschakelen door toe te voegen Hallo volgende `addonFeatures` sectie na Hallo `fabricSettings` zoals weergegeven in het volgende codefragment Hallo sectie:</span><span class="sxs-lookup"><span data-stu-id="8224e-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="8224e-117">Zodra u de sjabloon voor het cluster hebt bijgewerkt Hello voorgaande wijzigingen, ze toepassen en laten Hallo upgrade voltooid.</span><span class="sxs-lookup"><span data-stu-id="8224e-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="8224e-118">Hierna kunt Hallo DNS-systeemservice wordt gestart in het cluster die wordt aangeroepen `fabric:/System/DnsService` onder system service sectie in het Hallo Service Fabric explorer.</span><span class="sxs-lookup"><span data-stu-id="8224e-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="8224e-119">Ook kunt u DNS-service via de portal Hallo HALLO hallo gelijktijdig met maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="8224e-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="8224e-120">Hallo DNS-service kan worden ingeschakeld door het selectievakje voor Hallo `Include DNS service` in Hallo `Cluster configuration` menu zoals weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="8224e-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![DNS-service via de portal Hallo inschakelen][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="8224e-122">Hallo DNS-naam voor uw service instellen</span><span class="sxs-lookup"><span data-stu-id="8224e-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="8224e-123">Als Hallo DNS-service wordt uitgevoerd in uw cluster, kunt u instellen een DNS-naam voor uw services declaratief voor standaardservices in Hallo `ApplicationManifest.xml` of via Powershell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8224e-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="8224e-124">Hallo DNS-naam voor een standaardservice instellen in Hallo ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="8224e-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="8224e-125">Open het project in Visual Studio of uw favoriete editor en open Hallo `ApplicationManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="8224e-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="8224e-126">Ga toohello standaardsectie services, en voor elke service toevoegen Hallo `ServiceDnsName` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="8224e-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="8224e-127">Hallo volgende voorbeeld ziet u hoe tooset DNS-naam van de service hello te Hallo`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="8224e-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="8224e-128">Zodra de toepassing hello is geïmplementeerd, ziet u service-exemplaar in Service Fabric explorer Hallo HALLO hallo DNS-naam voor dit exemplaar zoals weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="8224e-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![Service-eindpunten][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="8224e-130">Hallo DNS-naam voor een service met behulp van Powershell instellen</span><span class="sxs-lookup"><span data-stu-id="8224e-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="8224e-131">U kunt Hallo DNS-naam voor een service instellen bij het maken met behulp van Hallo `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="8224e-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="8224e-132">Hallo volgende voorbeeld wordt een nieuwe staatloze service met Hallo DNS-naam`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="8224e-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a><span data-ttu-id="8224e-133">Met behulp van DNS in uw services</span><span class="sxs-lookup"><span data-stu-id="8224e-133">Using DNS in your services</span></span>
<span data-ttu-id="8224e-134">Als u meer dan één service implementeert, kunt u Hallo eindpunten van andere services toocommunicate met vinden met behulp van een DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="8224e-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="8224e-135">Hallo DNS-service is alleen van toepassing toostateless services, aangezien Hallo DNS-protocol kan niet met stateful services communiceren.</span><span class="sxs-lookup"><span data-stu-id="8224e-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="8224e-136">Voor stateful services, kunt u Hallo ingebouwde omgekeerde proxy voor HTTP-aanroepen toocall een bepaalde service-partitie.</span><span class="sxs-lookup"><span data-stu-id="8224e-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="8224e-137">Hallo volgende code toont hoe toocall een andere service, die is gewoon een gewone http aanroepen waarin u Hallo-poort en een optionele pad als onderdeel van het Hallo-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="8224e-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8224e-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8224e-138">Next steps</span></span>
<span data-ttu-id="8224e-139">Meer informatie over servicecommunicatie binnen een cluster met Hallo [verbinding maken en te communiceren met services](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="8224e-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
