---
title: Controleer aaaverify verkeer met Azure-netwerk-Watcher IP-flow - PowerShell | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd met behulp van PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f87af-103">Controleer of het verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met IP-stroom controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f87af-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f87af-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f87af-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f87af-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f87af-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f87af-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f87af-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f87af-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f87af-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f87af-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="f87af-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f87af-109">IP-stroom controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f87af-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="f87af-110">Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron- of back-end praten kunt.</span><span class="sxs-lookup"><span data-stu-id="f87af-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="f87af-111">IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="f87af-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f87af-112">Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="f87af-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f87af-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f87af-113">Before you begin</span></span>

<span data-ttu-id="f87af-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben.</span><span class="sxs-lookup"><span data-stu-id="f87af-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f87af-115">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="f87af-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f87af-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="f87af-116">Scenario</span></span>

<span data-ttu-id="f87af-117">Dit scenario maakt gebruik van IP-stroom tooverify verifiëren als een virtuele machine kunt praten tooa bekende Bing IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f87af-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="f87af-118">Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="f87af-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="f87af-119">toolearn meer over IP-stroom controleren, gaat u naar [IP-stroom overzicht controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f87af-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f87af-120">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f87af-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="f87af-121">de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f87af-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="f87af-122">Hallo `$networkWatcher` variabele is doorgegeven toohello IP stroom cmdlet controleren.</span><span class="sxs-lookup"><span data-stu-id="f87af-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="f87af-123">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="f87af-123">Get a VM</span></span>

<span data-ttu-id="f87af-124">IP-stroom controleren tests verkeer tooor van een IP-adres op een virtuele machine tooor vanaf een externe bestemming.</span><span class="sxs-lookup"><span data-stu-id="f87af-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="f87af-125">Een Id van een virtuele machine is vereist voor het Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f87af-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="f87af-126">Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="f87af-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="f87af-127">Hallo NIC's ophalen</span><span class="sxs-lookup"><span data-stu-id="f87af-127">Get hello NICS</span></span>

<span data-ttu-id="f87af-128">Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f87af-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="f87af-129">Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="f87af-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="f87af-130">Voer IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="f87af-130">Run IP flow verify</span></span>

<span data-ttu-id="f87af-131">Nu dat we Hallo informatie nodig toorun Hallo cmdlet hebben, voeren we Hallo `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest Hallo verkeer.</span><span class="sxs-lookup"><span data-stu-id="f87af-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="f87af-132">In dit voorbeeld gebruiken we Hallo eerste IP-adres op Hallo eerste NIC.</span><span class="sxs-lookup"><span data-stu-id="f87af-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="f87af-133">IP-stroom controleren vereist dat de VM-resource Hallo toorun wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f87af-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="f87af-134">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="f87af-134">Review Results</span></span>

<span data-ttu-id="f87af-135">Nadat u `Test-AzureRmNetworkWatcherIPFlow` Hallo resultaten worden geretourneerd, hello volgende voorbeeld is Hallo resultaten geretourneerd door de voorgaande stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f87af-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="f87af-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f87af-136">Next steps</span></span>

<span data-ttu-id="f87af-137">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f87af-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













