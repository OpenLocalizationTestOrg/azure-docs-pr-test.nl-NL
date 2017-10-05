---
title: "Controleer of verkeer verifiëren met Azure-netwerk-Watcher IP-flow - REST | Microsoft Docs"
description: Dit artikel wordt beschreven hoe u kunt controleren als verkeer naar of van een virtuele machine wordt toegestaan of geweigerd
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
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d89fa-103">Controleer of het verkeer wordt toegestaan of geweigerd met IP-stroom controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d89fa-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d89fa-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d89fa-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="d89fa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d89fa-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="d89fa-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d89fa-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="d89fa-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d89fa-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="d89fa-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="d89fa-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="d89fa-109">IP-stroom controleren is een functie van netwerk-Watcher die u controleren kunt of er verkeer is toegestaan naar of van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d89fa-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="d89fa-110">De validatie kan worden uitgevoerd voor binnenkomend of uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="d89fa-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="d89fa-111">Dit scenario is nuttig voor het ophalen van de huidige status of een virtuele machine contact met een externe bron of de back-end opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="d89fa-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="d89fa-112">IP-stroom controleren om te controleren of als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en problemen oplossen stromen die worden geblokkeerd door het NSG-regels kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d89fa-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d89fa-113">Een andere reden voor het gebruik van IP-stroom controleren om ervoor te zorgen verkeer dat u blokkeren wilt is goed door het NSG worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="d89fa-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d89fa-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d89fa-114">Before you begin</span></span>

<span data-ttu-id="d89fa-115">ARMclient wordt gebruikt voor het aanroepen van de REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d89fa-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="d89fa-116">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="d89fa-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="d89fa-117">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="d89fa-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d89fa-118">Scenario</span><span class="sxs-lookup"><span data-stu-id="d89fa-118">Scenario</span></span>

<span data-ttu-id="d89fa-119">Dit scenario maakt gebruik van IP-stroom controleren om te controleren of als een virtuele machine naar een andere computer via poort 443 communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="d89fa-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="d89fa-120">Als het verkeer wordt geweigerd, wordt de beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="d89fa-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="d89fa-121">Voor meer informatie over IP-stroom controleren, gaat u naar [IP-stroom overzicht controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d89fa-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="d89fa-122">In dit scenario u:</span><span class="sxs-lookup"><span data-stu-id="d89fa-122">In this scenario, you:</span></span>

* <span data-ttu-id="d89fa-123">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="d89fa-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="d89fa-124">Aanroep van IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="d89fa-124">Call IP flow verify</span></span>
* <span data-ttu-id="d89fa-125">Resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="d89fa-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="d89fa-126">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="d89fa-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="d89fa-127">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="d89fa-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="d89fa-128">Voer het volgende script om te retourneren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d89fa-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="d89fa-129">De volgende code moet waarden voor de variabelen:</span><span class="sxs-lookup"><span data-stu-id="d89fa-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="d89fa-130">**subscriptionId** -de abonnements-Id te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d89fa-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="d89fa-131">**resourceGroupName** -de naam van een resourcegroep die virtuele machines bevatten.</span><span class="sxs-lookup"><span data-stu-id="d89fa-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="d89fa-132">De informatie die nodig is de id onder het type `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="d89fa-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="d89fa-133">De resultaten moeten zijn vergelijkbaar met het volgende codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d89fa-133">The results should be similar to the following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="d89fa-134">Aanroep van IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="d89fa-134">Call IP flow Verify</span></span>

<span data-ttu-id="d89fa-135">Het volgende voorbeeld wordt een verzoek om te controleren of het verkeer voor een opgegeven virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d89fa-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="d89fa-136">Het antwoord retourneert als het verkeer wordt toegestaan of als het verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="d89fa-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="d89fa-137">Als verkeer wordt geweigerd dat ook wordt het verkeer wordt geblokkeerd door welke regel.</span><span class="sxs-lookup"><span data-stu-id="d89fa-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="d89fa-138">IP-stroom controleren vereist dat de VM-resource wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d89fa-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="d89fa-139">Het script is vereist voor de resource-Id van een virtuele machine en een netwerkinterfacekaart op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d89fa-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="d89fa-140">Deze waarden worden geleverd door de voorgaande uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d89fa-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="d89fa-141">De naam van de resourcegroep in de aanvraag-URI is voor alle netwerk-Watcher REST-aanroepen die het bevat de netwerk-Watcher-instantie, niet de bronnen die u wilt de diagnostische acties uitvoeren op.</span><span class="sxs-lookup"><span data-stu-id="d89fa-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

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

## <a name="understanding-the-results"></a><span data-ttu-id="d89fa-142">Inzicht in de resultaten</span><span class="sxs-lookup"><span data-stu-id="d89fa-142">Understanding the results</span></span>

<span data-ttu-id="d89fa-143">Het antwoord dat u terughalen vertelt u of het verkeer wordt toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="d89fa-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="d89fa-144">Het antwoord ziet eruit als een van de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="d89fa-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="d89fa-145">**Toegestaan**</span><span class="sxs-lookup"><span data-stu-id="d89fa-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="d89fa-146">**Geweigerd**</span><span class="sxs-lookup"><span data-stu-id="d89fa-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="d89fa-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d89fa-147">Next steps</span></span>

<span data-ttu-id="d89fa-148">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) voor meer informatie over Netwerkbeveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="d89fa-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












