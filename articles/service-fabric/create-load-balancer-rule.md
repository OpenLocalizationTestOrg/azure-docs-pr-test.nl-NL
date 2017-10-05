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
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="ac333-103">Open poorten voor een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="ac333-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="ac333-104">De load balancer geïmplementeerd met uw Azure Service Fabric-cluster stuurt het verkeer naar uw app uitgevoerd op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ac333-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="ac333-105">Als u uw app voor het gebruik van een andere poort wijzigt, moet u die poort (of een andere poort routeren) in de Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ac333-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="ac333-106">Wanneer u uw service fabric-cluster naar Azure hebt geïmplementeerd, kan een load balancer automatisch voor u is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ac333-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="ac333-107">Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac333-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="ac333-108">Het service fabric configureren</span><span class="sxs-lookup"><span data-stu-id="ac333-108">Configure service fabric</span></span>

<span data-ttu-id="ac333-109">Service Fabric-toepassing **ServiceManifest.xml** config-bestand definieert de eindpunten wordt verwacht dat uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac333-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="ac333-110">Nadat het configuratiebestand is bijgewerkt om te definiëren van een eindpunt en de load balancer moet worden bijgewerkt als u wilt weergeven die (of een andere) poort.</span><span class="sxs-lookup"><span data-stu-id="ac333-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="ac333-111">Zie voor meer informatie over het maken van het service fabric-eindpunt [Setup een eindpunt](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ac333-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="ac333-112">Een load balancer-regel maken</span><span class="sxs-lookup"><span data-stu-id="ac333-112">Create a load balancer rule</span></span>

<span data-ttu-id="ac333-113">Een load balancer-regel wordt een internetgerichte poort geopend en stuurt het verkeer naar het interne knooppunt poort wordt gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac333-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="ac333-114">Als u een load balancer niet hebt, raadpleegt u [een internetgerichte load balancer configureren](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac333-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="ac333-115">U moet de volgende informatie verzamelen voor het maken van een load balancer-regel:</span><span class="sxs-lookup"><span data-stu-id="ac333-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="ac333-116">Naam van load balancer.</span><span class="sxs-lookup"><span data-stu-id="ac333-116">Load balancer name.</span></span>
- <span data-ttu-id="ac333-117">De resourcegroep van de load balancer en service fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="ac333-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="ac333-118">Externe poort.</span><span class="sxs-lookup"><span data-stu-id="ac333-118">External port.</span></span>
- <span data-ttu-id="ac333-119">Interne poort.</span><span class="sxs-lookup"><span data-stu-id="ac333-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="ac333-120">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ac333-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="ac333-121">Als u moet de naam van de load balancer bepalen, gebruikt u deze opdracht om snel een lijst van alle load balancers en de bijbehorende resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ac333-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="ac333-122">Dit duurt slechts één opdracht voor het maken van een regel voor load balancer met de **Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="ac333-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="ac333-123">Alleen moet u beide de naam van de load balancer en resource groep om een nieuwe regel te maken.</span><span class="sxs-lookup"><span data-stu-id="ac333-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="ac333-124">De Azure CLI-opdracht heeft een aantal parameters die worden beschreven in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="ac333-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="ac333-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="ac333-125">Parameter</span></span> | <span data-ttu-id="ac333-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ac333-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="ac333-127">De poort van de service fabric-toepassing luistert.</span><span class="sxs-lookup"><span data-stu-id="ac333-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="ac333-128">De poort van de load balancer wordt voor externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ac333-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="ac333-129">De naam van de load balancer wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ac333-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="ac333-130">De resourcegroep met de load balancer en de service fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="ac333-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="ac333-131">De naam van de regel hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="ac333-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="ac333-132">Zie voor meer informatie over het maken van een load balancer met de Azure CLI [een load balancer maken met de Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ac333-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="ac333-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac333-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="ac333-134">Als u moet de naam van de load balancer bepalen, gebruikt u deze opdracht om snel een lijst met alle load balancers en bijbehorende resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ac333-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="ac333-135">PowerShell is iets gecompliceerder dan de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ac333-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="ac333-136">Conceptueel gezien, komen de volgende stappen uit om een regel te maken.</span><span class="sxs-lookup"><span data-stu-id="ac333-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="ac333-137">De load balancer ophalen uit Azure.</span><span class="sxs-lookup"><span data-stu-id="ac333-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="ac333-138">Een regel maken.</span><span class="sxs-lookup"><span data-stu-id="ac333-138">Create a rule.</span></span>
3. <span data-ttu-id="ac333-139">De regel toevoegen aan de load balancer.</span><span class="sxs-lookup"><span data-stu-id="ac333-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="ac333-140">De load balancer bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ac333-140">Update the load balancer.</span></span>

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

<span data-ttu-id="ac333-141">Met betrekking tot de `New-AzureRmLoadBalancerRuleConfig` opdracht, de `-FrontendPort` vertegenwoordigt de poort die de load balancer voor externe verbindingen wordt en de `-BackendPort` vertegenwoordigt de poort die de service fabric-app wordt beluisterd.</span><span class="sxs-lookup"><span data-stu-id="ac333-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="ac333-142">Zie voor meer informatie over het maken van een load balancer met PowerShell [een load balancer maken met PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ac333-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

