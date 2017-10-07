---
title: Controleer aaaVerify verkeer met Azure-netwerk-Watcher IP-flow - REST | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="34a13-103">Controleer of het verkeer wordt toegestaan of geweigerd met IP-stroom controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="34a13-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="34a13-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34a13-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="34a13-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a13-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="34a13-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="34a13-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="34a13-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34a13-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="34a13-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="34a13-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="34a13-109">IP-stroom controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34a13-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="34a13-110">Hallo validatie kan worden uitgevoerd voor binnenkomend of uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="34a13-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="34a13-111">Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron- of back-end praten kunt.</span><span class="sxs-lookup"><span data-stu-id="34a13-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="34a13-112">IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="34a13-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="34a13-113">Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="34a13-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34a13-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="34a13-114">Before you begin</span></span>

<span data-ttu-id="34a13-115">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34a13-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="34a13-116">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="34a13-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="34a13-117">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="34a13-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="34a13-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="34a13-118">Scenario</span></span>

<span data-ttu-id="34a13-119">Dit scenario maakt gebruik van IP-stroom controleren tooverify als een virtuele machine tooanother computer via poort 443 communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="34a13-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="34a13-120">Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="34a13-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="34a13-121">toolearn meer over IP-stroom controleren, gaat u naar [IP-stroom overzicht controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="34a13-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="34a13-122">In dit scenario u:</span><span class="sxs-lookup"><span data-stu-id="34a13-122">In this scenario, you:</span></span>

* <span data-ttu-id="34a13-123">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="34a13-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="34a13-124">Aanroep van IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="34a13-124">Call IP flow verify</span></span>
* <span data-ttu-id="34a13-125">Resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="34a13-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="34a13-126">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="34a13-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="34a13-127">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="34a13-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="34a13-128">Hallo script tooreturn na een virtuele machine uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="34a13-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="34a13-129">Hallo moet volgende code waarden voor Hallo variabelen:</span><span class="sxs-lookup"><span data-stu-id="34a13-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="34a13-130">**subscriptionId** -Hallo toouse voor abonnement-Id.</span><span class="sxs-lookup"><span data-stu-id="34a13-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="34a13-131">**resourceGroupName** - hello naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="34a13-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="34a13-132">Hallo informatie die nodig is Hallo-id onder Hallo type `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="34a13-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="34a13-133">Hallo resultaten moeten vergelijkbaar toohello codevoorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="34a13-133">hello results should be similar toohello following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="34a13-134">Aanroep van IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="34a13-134">Call IP flow Verify</span></span>

<span data-ttu-id="34a13-135">Hallo wordt volgende voorbeeld een aanvraag tooverify Hallo verkeer voor een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34a13-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="34a13-136">antwoord Hallo retourneert als Hallo verkeer wordt toegestaan of als het Hallo-verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="34a13-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="34a13-137">Als verkeer wordt geweigerd dat deze ook welke regel blokkeert verkeer Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="34a13-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="34a13-138">IP-stroom controleren vereist dat de VM-resource hello wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="34a13-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="34a13-139">Hallo script vereist Hallo resource-Id van een virtuele machine en een netwerkinterfacekaart op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34a13-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="34a13-140">Deze waarden worden geleverd door Hallo voorafgaand aan de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="34a13-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="34a13-141">Voor alle netwerk-Watcher REST Hallo aanroepen Resourcegroepnaam in Hallo aanvraag-URI is Hallo een bestand met de Hallo netwerk-Watcher-exemplaar niet Hallo resources u Hallo diagnostische acties uitvoert op.</span><span class="sxs-lookup"><span data-stu-id="34a13-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a><span data-ttu-id="34a13-142">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="34a13-142">Understanding hello results</span></span>

<span data-ttu-id="34a13-143">antwoord Hallo die u terughalen vertelt u of Hallo verkeer wordt toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="34a13-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="34a13-144">antwoord Hallo ziet eruit als een van de Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="34a13-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="34a13-145">**Toegestaan**</span><span class="sxs-lookup"><span data-stu-id="34a13-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="34a13-146">**Geweigerd**</span><span class="sxs-lookup"><span data-stu-id="34a13-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="34a13-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34a13-147">Next steps</span></span>

<span data-ttu-id="34a13-148">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn meer over Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="34a13-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












