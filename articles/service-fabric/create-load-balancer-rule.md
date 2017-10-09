---
title: een Azure Load Balancer-regel voor een cluster aaaCreate
description: Een Azure Load Balancer tooopen poorten voor uw Azure Service Fabric-cluster configureren.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Open poorten voor een Service Fabric-cluster

Hallo load balancer geïmplementeerd met uw Azure Service Fabric-cluster stuurt verkeer tooyour app die op een knooppunt wordt uitgevoerd. Als u uw app toouse een andere poort wijzigt, moet u die poort (of een andere poort routeren) in hello Azure Load Balancer.

Wanneer u uw service fabric-cluster tooAzure hebt geïmplementeerd, kan een load balancer automatisch voor u is gemaakt. Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Het service fabric configureren

Service Fabric-toepassing **ServiceManifest.xml** configuratiebestand definieert het Hallo-eindpunten die uw toepassing toouse wordt verwacht. Nadat het Hallo-configuratiebestand is bijgewerkte toodefine een eindpunt, Hallo load balancer moet bijgewerkte tooexpose die (of een ander) poort. Zie voor meer informatie over hoe toocreate service fabric-eindpunt hello, [Setup een eindpunt](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Een load balancer-regel maken

Een load balancer-regel wordt een internetgerichte poort geopend en stuurt verkeer toohello interne van knooppunt poort wordt gebruikt door uw toepassing. Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).

toocreate een load balancer-regel moet u toocollect Hallo volgende informatie:

- Naam van load balancer.
- Resourcegroep Hallo load balancer en service fabric-cluster.
- Externe poort.
- Interne poort.

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>Als u toodetermine Hallo naam Hallo load balancer moet, gebruikt u deze opdracht tooquickly get een lijst met alle load balancers en de resourcegroepen Hallo die zijn gekoppeld.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Het duurt maar een toocreate één opdracht een load balancer-regel Hello **Azure CLI**. U hoeft alleen maar tooknow zowel Hallo-naam van Hallo load balancer en resource groep toocreate een nieuwe regel.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hello Azure CLI-opdracht heeft een aantal parameters die worden beschreven in de volgende tabel Hallo:

| Parameter | Beschrijving |
| --------- | ----------- |
| `--backend-port`  | Hallo poort Hallo service fabric-toepassing luistert. |
| `--frontend-port` | Hallo poort Hallo load balancer zichtbaar gemaakt voor externe verbindingen. |
| `-lb-name` | Hallo-naam van Hallo balancer toochange laden. |
| `-g`       | Hallo-resourcegroep die Hallo load balancer- en service fabric-cluster. |
| `-n`       | Hallo gekozen naam van regel Hallo. |


>[!NOTE]
>Voor meer informatie over hoe toocreate een load balancer Hello Azure CLI zien [een load balancer maken met Azure CLI Hallo](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Als u toodetermine Hallo naam Hallo load balancer moet, gebruikt u deze opdracht tooquickly get een lijst met alle load balancers en bijbehorende resourcegroepen.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell is iets gecompliceerder dan hello Azure CLI. Conceptueel gezien doen Hallo toocreate stappen te volgen, een regel.

1. Hallo load balancer ophalen uit Azure.
2. Een regel maken.
3. Hallo regel toohello load balancer toevoegen.
4. Hallo load balancer bijwerken.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Met betrekking tot Hallo `New-AzureRmLoadBalancerRuleConfig` opdracht hello `-FrontendPort` vertegenwoordigt Hallo poort Hallo load balancer wordt voor externe verbindingen en Hallo `-BackendPort` vertegenwoordigt Hallo poort Hallo service fabric-app wordt beluisterd.

>[!NOTE]
>Voor meer informatie over hoe toocreate een load balancer met PowerShell, Zie [een load balancer maken met PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

