---
title: Controleer of verkeer met Azure-netwerk-Watcher IP-stroom controleren of - Azure-portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe u kunt controleren als verkeer naar of van een virtuele machine wordt toegestaan of geweigerd
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
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="e1020-103">Controleer als verkeer wordt toegestaan of geweigerd naar of van een virtuele machine met het IP-stromen controleren of een onderdeel van Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="e1020-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e1020-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e1020-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="e1020-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1020-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="e1020-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e1020-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="e1020-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e1020-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="e1020-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="e1020-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="e1020-109">IP-stroom controleren is een functie van netwerk-Watcher die u controleren kunt of er verkeer is toegestaan naar of van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e1020-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="e1020-110">De validatie kan worden uitgevoerd voor binnenkomend of uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="e1020-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="e1020-111">Dit scenario is nuttig voor het ophalen van de huidige status of een virtuele machine contact met een externe resource of een andere bron opnemen kunt.</span><span class="sxs-lookup"><span data-stu-id="e1020-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="e1020-112">IP-stroom controleren om te controleren of als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en problemen oplossen stromen die worden geblokkeerd door het NSG-regels kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e1020-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="e1020-113">Een andere reden voor het gebruik van IP-stroom controleren om ervoor te zorgen verkeer dat u blokkeren wilt is goed door het NSG worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e1020-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e1020-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="e1020-114">Before you begin</span></span>

<span data-ttu-id="e1020-115">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben.</span><span class="sxs-lookup"><span data-stu-id="e1020-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="e1020-116">Het scenario wordt ervan uitgegaan dat er een resourcegroep met een geldige virtuele machine bestaat om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e1020-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e1020-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="e1020-117">Scenario</span></span>

<span data-ttu-id="e1020-118">Dit scenario maakt gebruik van IP-stromen controleren om te controleren of als een virtuele machine naar een andere computer via poort 443 communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="e1020-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="e1020-119">Als het verkeer wordt geweigerd, wordt de beveiligingsregel die dat verkeer wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="e1020-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="e1020-120">Voor meer informatie over IP-stromen controleren, gaat u naar [overzicht van IP-stromen controleren](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e1020-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="e1020-121">Voer IP-stroom controleren</span><span class="sxs-lookup"><span data-stu-id="e1020-121">Run IP flow verify</span></span>

<span data-ttu-id="e1020-122">Navigeer naar uw netwerk-Watcher en klikt u op **IP-stroom controleren**.</span><span class="sxs-lookup"><span data-stu-id="e1020-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="e1020-123">Selecteer de virtuele machine en u wilt controleren of het verkeer van netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="e1020-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="e1020-124">Voer eventueel aanvullende informatie voor het filteren en klik op **controleren**.</span><span class="sxs-lookup"><span data-stu-id="e1020-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="e1020-125">Nadat u op **controleren**, de stroom op basis van de criteria die u hebt opgegeven is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e1020-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="e1020-126">Het resultaat is een **toegang is toegestaan** of **toegang is geweigerd**.</span><span class="sxs-lookup"><span data-stu-id="e1020-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="e1020-127">Als de toegang is geweigerd, wordt de Netwerkbeveiligingsgroep (NSG) en beveiliging regel die verkeer blokkeren opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e1020-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="e1020-128">Als de DOS-verkeer verwacht gedrag is, zijn de regel is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="e1020-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="e1020-129">IP-stroom controleren vereist dat de VM-resource wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e1020-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="e1020-130">Als u in de volgende afbeelding zien kunt, wordt het uitgaande HTTPS-verkeer is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e1020-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![IP-stroom overzicht controleren][1]

<span data-ttu-id="e1020-132">Zoals u in de volgende afbeelding, verkeer wordt gewijzigd naar inkomende en de binnenkomende poort 123 gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e1020-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="e1020-133">Verkeer wordt nu geweigerd, het bericht 'Toegang geweigerd' is opgegeven samen met de opgegeven groep en beveiliging netwerkbeveiligingsregel die door het verkeer geweigerd.</span><span class="sxs-lookup"><span data-stu-id="e1020-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![IP-stroom resultaten][2]

## <a name="next-steps"></a><span data-ttu-id="e1020-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e1020-135">Next steps</span></span>

<span data-ttu-id="e1020-136">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) voor het opsporen van de groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e1020-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













