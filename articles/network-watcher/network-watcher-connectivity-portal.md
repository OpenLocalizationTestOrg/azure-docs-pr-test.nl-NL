---
title: aaaCheck connectiviteit met de Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toouse connectiviteit contact op met de netwerk-Watcher met hello Azure-portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="e4606-103">Controleer de verbinding met de netwerk-Watcher van Azure met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e4606-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e4606-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e4606-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="e4606-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4606-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="e4606-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e4606-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="e4606-107">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="e4606-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="e4606-108">Meer informatie over hoe toouse connectiviteit tooverify als een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt kan worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="e4606-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e4606-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="e4606-109">Before you begin</span></span>

<span data-ttu-id="e4606-110">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="e4606-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="e4606-111">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt toocheck connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="e4606-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="e4606-112">Virtuele machines toocheck connectiviteit met.</span><span class="sxs-lookup"><span data-stu-id="e4606-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4606-113">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="e4606-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="e4606-114">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="e4606-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="e4606-115">Controleer de connectiviteit tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e4606-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="e4606-116">In dit voorbeeld controleert connectiviteit tooa bestemde virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="e4606-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="e4606-117">Navigeer tooyour netwerk-Watcher en klik op **connectiviteit selectievakje (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="e4606-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="e4606-118">Selecteer Hallo virtuele machine vanaf toocheck verbinding.</span><span class="sxs-lookup"><span data-stu-id="e4606-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="e4606-119">In Hallo **bestemming** sectie kiezen **Selecteer een virtuele machine** en kies Hallo juiste virtuele machine en poort tootest.</span><span class="sxs-lookup"><span data-stu-id="e4606-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="e4606-120">Nadat u op **controleren**, Hallo connectiviteit tussen Hallo virtuele machines op de opgegeven poort voor Hallo worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="e4606-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="e4606-121">In voorbeeld Hallo Hallo bestemming VM is niet bereikbaar, een overzicht van hops worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4606-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Resultaten van de verbinding voor een virtuele machine][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="e4606-123">Controleer de verbindingen van het externe eindpunt</span><span class="sxs-lookup"><span data-stu-id="e4606-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="e4606-124">toocheck hello connectiviteit en latentie tooa externe eindpunt, kies Hallo **handmatig opgeven** keuzerondje in Hallo **bestemming** sectie, invoer Hallo-url en Hallo-poort en klik op **controleren** .</span><span class="sxs-lookup"><span data-stu-id="e4606-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="e4606-125">Dit wordt gebruikt voor externe eindpunten zoals websites en -opslag-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e4606-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Resultaten van de verbinding voor een website][2]

## <a name="next-steps"></a><span data-ttu-id="e4606-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4606-127">Next steps</span></span>

<span data-ttu-id="e4606-128">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="e4606-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="e4606-129">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e4606-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
