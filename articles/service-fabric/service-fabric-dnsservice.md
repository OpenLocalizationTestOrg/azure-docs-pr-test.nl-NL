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
# <a name="dns-service-in-azure-service-fabric"></a>DNS-Service in Azure Service Fabric
Hallo DNS-Service is een optionele systeemservice die u in uw cluster toodiscover inschakelen kunt andere services Hallo DNS-protocol gebruiken.

Veel services, vooral beperkte services, een bestaande URL-naam en wordt kunnen tooresolve hebben ze wenselijk, met name in 'lift- en verschuiven'-scenario's voor het gebruik van Hallo standaard DNS-protocol (in plaats van Hallo Naming Service protocol) is. Hallo DNS-service kunt u toomap DNS-namen tooa servicenaam en daarom los eindpunt IP-adressen. 

Hallo DNS-service wijst DNS-namen tooservice namen, die op zijn beurt worden opgelost door Hallo Naming Service tooreturn Hallo service-eindpunt. Hallo DNS-naam voor het Hallo-service is opgegeven op Hallo moment gemaakt. 

![Service-eindpunten][0]

## <a name="enabling-hello-dns-service"></a>Hallo DNS-service inschakelen
U moet eerst tooenable Hallo DNS-service in uw cluster. Hallo sjabloon ophalen voor Hallo-cluster dat u wilt dat toodeploy. U kunt beide Hallo gebruik [voorbeeldsjablonen](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) of een Resource Manager-sjabloon maken. U kunt Hallo DNS-service inschakelen met Hallo stappen te volgen:

1. Controleer dat Hallo `apiversion` te is ingesteld,`2017-07-01-preview` voor Hallo `Microsoft.ServiceFabric/clusters` resource, en als dat niet bijwerken zoals weergegeven in het volgende codefragment Hallo:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Nu Hallo DNS-service inschakelen door toe te voegen Hallo volgende `addonFeatures` sectie na Hallo `fabricSettings` zoals weergegeven in het volgende codefragment Hallo sectie: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Zodra u de sjabloon voor het cluster hebt bijgewerkt Hello voorgaande wijzigingen, ze toepassen en laten Hallo upgrade voltooid. Hierna kunt Hallo DNS-systeemservice wordt gestart in het cluster die wordt aangeroepen `fabric:/System/DnsService` onder system service sectie in het Hallo Service Fabric explorer. 

Ook kunt u DNS-service via de portal Hallo HALLO hallo gelijktijdig met maken van het cluster. Hallo DNS-service kan worden ingeschakeld door het selectievakje voor Hallo `Include DNS service` in Hallo `Cluster configuration` menu zoals weergegeven in de volgende schermafbeelding Hallo:

![DNS-service via de portal Hallo inschakelen][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Hallo DNS-naam voor uw service instellen
Als Hallo DNS-service wordt uitgevoerd in uw cluster, kunt u instellen een DNS-naam voor uw services declaratief voor standaardservices in Hallo `ApplicationManifest.xml` of via Powershell-opdrachten.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Hallo DNS-naam voor een standaardservice instellen in Hallo ApplicationManifest.xml
Open het project in Visual Studio of uw favoriete editor en open Hallo `ApplicationManifest.xml` bestand. Ga toohello standaardsectie services, en voor elke service toevoegen Hallo `ServiceDnsName` kenmerk. Hallo volgende voorbeeld ziet u hoe tooset DNS-naam van de service hello te Hallo`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Zodra de toepassing hello is geïmplementeerd, ziet u service-exemplaar in Service Fabric explorer Hallo HALLO hallo DNS-naam voor dit exemplaar zoals weergegeven in de volgende afbeelding Hallo: 

![Service-eindpunten][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Hallo DNS-naam voor een service met behulp van Powershell instellen
U kunt Hallo DNS-naam voor een service instellen bij het maken met behulp van Hallo `New-ServiceFabricService` Powershell. Hallo volgende voorbeeld wordt een nieuwe staatloze service met Hallo DNS-naam`service1.application1`

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

## <a name="using-dns-in-your-services"></a>Met behulp van DNS in uw services
Als u meer dan één service implementeert, kunt u Hallo eindpunten van andere services toocommunicate met vinden met behulp van een DNS-naam. Hallo DNS-service is alleen van toepassing toostateless services, aangezien Hallo DNS-protocol kan niet met stateful services communiceren. Voor stateful services, kunt u Hallo ingebouwde omgekeerde proxy voor HTTP-aanroepen toocall een bepaalde service-partitie.

Hallo volgende code toont hoe toocall een andere service, die is gewoon een gewone http aanroepen waarin u Hallo-poort en een optionele pad als onderdeel van het Hallo-URL opgeven.

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

## <a name="next-steps"></a>Volgende stappen
Meer informatie over servicecommunicatie binnen een cluster met Hallo [verbinding maken en te communiceren met services](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
