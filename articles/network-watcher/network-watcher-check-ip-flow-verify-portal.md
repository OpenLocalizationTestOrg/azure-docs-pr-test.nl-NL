---
title: Controleer aaaVerify verkeer met Azure-netwerk-Watcher IP-flow - Azure-portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f65d2-103">Controleer als verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met het IP-stromen controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="f65d2-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f65d2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f65d2-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f65d2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f65d2-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f65d2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f65d2-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f65d2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f65d2-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f65d2-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="f65d2-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f65d2-109">IP-stroom controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f65d2-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="f65d2-110">Hallo validatie kan worden uitgevoerd voor binnenkomend of uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="f65d2-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="f65d2-111">Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron of een andere resource praten kunt.</span><span class="sxs-lookup"><span data-stu-id="f65d2-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="f65d2-112">IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="f65d2-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f65d2-113">Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="f65d2-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f65d2-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f65d2-114">Before you begin</span></span>

<span data-ttu-id="f65d2-115">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben.</span><span class="sxs-lookup"><span data-stu-id="f65d2-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f65d2-116">Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.</span><span class="sxs-lookup"><span data-stu-id="f65d2-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f65d2-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="f65d2-117">Scenario</span></span>

<span data-ttu-id="f65d2-118">Dit scenario maakt gebruik van IP-stromen controleren tooverify als een virtuele machine tooanother computer via poort 443 communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="f65d2-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="f65d2-119">Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="f65d2-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="f65d2-120">toolearn meer informatie over IP-stromen controleren, gaat u naar [overzicht van IP-stromen controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f65d2-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="f65d2-121">Voer IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="f65d2-121">Run IP flow verify</span></span>

<span data-ttu-id="f65d2-122">Navigeer tooyour netwerk-Watcher en klik op **IP-stroom controleren**.</span><span class="sxs-lookup"><span data-stu-id="f65d2-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="f65d2-123">Hallo virtuele machine en netwerkinterface die u verkeer van tooverify wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f65d2-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="f65d2-124">Voer eventueel aanvullende informatie voor het filteren en klik op **controleren**.</span><span class="sxs-lookup"><span data-stu-id="f65d2-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="f65d2-125">Nadat u op **controleren**, op basis van Hallo criteria die u hebt opgegeven Hallo-stroom is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f65d2-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="f65d2-126">Hallo-resultaat is een **toegang is toegestaan** of **toegang is geweigerd**.</span><span class="sxs-lookup"><span data-stu-id="f65d2-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="f65d2-127">Als de toegang is geweigerd Hallo Netwerkbeveiligingsgroep (NSG) en beveiligingsregel die verkeer blokkeren is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f65d2-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="f65d2-128">Als Hallo DOS-verkeer verwacht gedrag is, zijn Hallo-regel is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="f65d2-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="f65d2-129">IP-stroom controleren vereist dat de VM-resource hello wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f65d2-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="f65d2-130">Als u in Hallo volgende afbeelding zien kunt, is Hallo uitgaande HTTPS-verkeer toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f65d2-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![IP-stroom overzicht controleren][1]

<span data-ttu-id="f65d2-132">Zoals u in Hallo installatiekopie te volgen, verkeer wordt gewijzigd tooinbound en Hallo inkomende too123 poort gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f65d2-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="f65d2-133">Verkeer wordt nu geweigerd, is Hallo-bericht 'Toegang geweigerd' opgegeven samen met de Hallo groep en beveiliging netwerkbeveiligingsregel die Hallo verkeer weigeren.</span><span class="sxs-lookup"><span data-stu-id="f65d2-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![IP-stroom resultaten][2]

## <a name="next-steps"></a><span data-ttu-id="f65d2-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f65d2-135">Next steps</span></span>

<span data-ttu-id="f65d2-136">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f65d2-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













