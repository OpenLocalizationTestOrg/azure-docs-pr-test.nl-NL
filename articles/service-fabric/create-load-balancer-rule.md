---
title: Een Azure Load Balancer-regel voor een cluster maken
description: Een Azure Load Balancer voor het openen van poorten voor uw Azure Service Fabric-cluster configureren.
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Open poorten voor een Service Fabric-cluster

De load balancer geïmplementeerd met uw Azure Service Fabric-cluster stuurt het verkeer naar uw app uitgevoerd op een knooppunt. Als u uw app voor het gebruik van een andere poort wijzigt, moet u die poort (of een andere poort routeren) in de Azure Load Balancer.

Wanneer u uw service fabric-cluster naar Azure hebt geïmplementeerd, kan een load balancer automatisch voor u is gemaakt. Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Het service fabric configureren

Service Fabric-toepassing **ServiceManifest.xml** config-bestand definieert de eindpunten wordt verwacht dat uw toepassing gebruiken. Nadat het configuratiebestand is bijgewerkt om te definiëren van een eindpunt en de load balancer moet worden bijgewerkt als u wilt weergeven die (of een andere) poort. Zie voor meer informatie over het maken van het service fabric-eindpunt [Setup een eindpunt](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Een load balancer-regel maken

Een load balancer-regel wordt een internetgerichte poort geopend en stuurt het verkeer naar het interne knooppunt poort wordt gebruikt door uw toepassing. Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).

U moet de volgende informatie verzamelen voor het maken van een load balancer-regel:

- Naam van load balancer.
- De resourcegroep van de load balancer en service fabric-cluster.
- Externe poort.
- Interne poort.

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>Als u moet de naam van de load balancer bepalen, gebruikt u deze opdracht om snel een lijst van alle load balancers en de bijbehorende resourcegroepen.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Dit duurt slechts één opdracht voor het maken van een regel voor load balancer met de **Azure CLI**. Alleen moet u beide de naam van de load balancer en resource groep om een nieuwe regel te maken.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

De Azure CLI-opdracht heeft een aantal parameters die worden beschreven in de volgende tabel:

| Parameter | Beschrijving |
| --------- | ----------- |
| `--backend-port`  | De poort van de service fabric-toepassing luistert. |
| `--frontend-port` | De poort van de load balancer wordt voor externe verbindingen. |
| `-lb-name` | De naam van de load balancer wijzigen. |
| `-g`       | De resourcegroep met de load balancer en de service fabric-cluster. |
| `-n`       | De naam van de regel hebt gekozen. |


>[!NOTE]
>Zie voor meer informatie over het maken van een load balancer met de Azure CLI [een load balancer maken met de Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Als u moet de naam van de load balancer bepalen, gebruikt u deze opdracht om snel een lijst met alle load balancers en bijbehorende resourcegroepen.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell is iets gecompliceerder dan de Azure CLI. Conceptueel gezien, komen de volgende stappen uit om een regel te maken.

1. De load balancer ophalen uit Azure.
2. Een regel maken.
3. De regel toevoegen aan de load balancer.
4. De load balancer bijwerken.

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Met betrekking tot de `New-AzureRmLoadBalancerRuleConfig` opdracht, de `-FrontendPort` vertegenwoordigt de poort die de load balancer voor externe verbindingen wordt en de `-BackendPort` vertegenwoordigt de poort die de service fabric-app wordt beluisterd.

>[!NOTE]
>Zie voor meer informatie over het maken van een load balancer met PowerShell [een load balancer maken met PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

