---
title: "aaaVerify verkeer met Azure-netwerk-Watcher IP-stromen verifiëren - Azure CLI | Microsoft Docs"
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd met Azure CLI
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="bd154-103">Controleer als verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met het IP-stromen controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="bd154-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bd154-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd154-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="bd154-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd154-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="bd154-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bd154-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="bd154-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bd154-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="bd154-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="bd154-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="bd154-109">IP-stromen controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bd154-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="bd154-110">Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron- of back-end praten kunt.</span><span class="sxs-lookup"><span data-stu-id="bd154-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="bd154-111">IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="bd154-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="bd154-112">Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="bd154-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="bd154-113">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="bd154-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd154-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bd154-114">Before you begin</span></span>

<span data-ttu-id="bd154-115">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben.</span><span class="sxs-lookup"><span data-stu-id="bd154-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="bd154-116">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="bd154-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="bd154-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="bd154-117">Scenario</span></span>

<span data-ttu-id="bd154-118">Dit scenario maakt gebruik van IP-stromen controleren tooverify als een virtuele machine tooa bekende praten kunt Bing IP-adres.</span><span class="sxs-lookup"><span data-stu-id="bd154-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="bd154-119">Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="bd154-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="bd154-120">toolearn meer informatie over IP-stromen controleren, gaat u naar [overzicht van IP-stromen controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd154-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="bd154-121">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="bd154-121">Get a VM</span></span>

<span data-ttu-id="bd154-122">IP-stroom controleren tests verkeer tooor van een IP-adres op een virtuele machine tooor vanaf een externe bestemming.</span><span class="sxs-lookup"><span data-stu-id="bd154-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="bd154-123">Een Id van een virtuele machine is vereist voor het Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd154-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="bd154-124">Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="bd154-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="bd154-125">Hallo NIC's ophalen</span><span class="sxs-lookup"><span data-stu-id="bd154-125">Get hello NICS</span></span>

<span data-ttu-id="bd154-126">Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="bd154-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="bd154-127">Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="bd154-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="bd154-128">Voer IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="bd154-128">Run IP flow verify</span></span>

<span data-ttu-id="bd154-129">Nu dat we Hallo informatie nodig toorun Hallo cmdlet hebben, voeren we Hallo `network watcher ip-flow-verify` cmdlet tootest Hallo verkeer.</span><span class="sxs-lookup"><span data-stu-id="bd154-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="bd154-130">In dit voorbeeld gebruiken we Hallo eerste IP-adres op Hallo eerste NIC.</span><span class="sxs-lookup"><span data-stu-id="bd154-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="bd154-131">IP-stromen controleren vereist dat de VM-resource Hallo toorun wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bd154-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="bd154-132">Resultaten bekijken</span><span class="sxs-lookup"><span data-stu-id="bd154-132">Review Results</span></span>

<span data-ttu-id="bd154-133">Nadat u `network watcher ip-flow-verify` Hallo resultaten worden geretourneerd, hello volgende voorbeeld is Hallo resultaten geretourneerd door de voorgaande stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd154-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="bd154-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd154-134">Next steps</span></span>

<span data-ttu-id="bd154-135">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bd154-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="bd154-136">Meer tooaudit uw NSG-instellingen in via [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd154-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
