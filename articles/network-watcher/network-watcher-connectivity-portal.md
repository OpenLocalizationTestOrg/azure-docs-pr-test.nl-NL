---
title: Controleer de verbinding met Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u verbinding met de netwerk-Watcher met de Azure portal gebruiken
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
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="b51dc-103">Controleer de verbinding met de netwerk-Watcher van Azure met Azure portal</span><span class="sxs-lookup"><span data-stu-id="b51dc-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b51dc-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b51dc-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="b51dc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b51dc-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="b51dc-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b51dc-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="b51dc-107">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="b51dc-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="b51dc-108">Informatie over het gebruik van verbinding om te controleren als direct TCP-verbinding van een virtuele machine naar een opgegeven eindpunt kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b51dc-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b51dc-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b51dc-109">Before you begin</span></span>

<span data-ttu-id="b51dc-110">In dit artikel wordt ervan uitgegaan dat u hebt de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="b51dc-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="b51dc-111">Een exemplaar van netwerk-Watcher in de regio die u wilt controleren, connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b51dc-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="b51dc-112">Virtuele machines connectiviteit met controleren.</span><span class="sxs-lookup"><span data-stu-id="b51dc-112">Virtual machines to check connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b51dc-113">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="b51dc-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="b51dc-114">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="b51dc-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="b51dc-115">Controleer de verbinding met een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b51dc-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="b51dc-116">In dit voorbeeld controleert de verbinding met een doel-virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="b51dc-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="b51dc-117">Navigeer naar uw netwerk-Watcher en klikt u op **connectiviteit selectievakje (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="b51dc-117">Navigate to your Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="b51dc-118">Selecteer de virtuele machine, Controleer de verbinding tussen.</span><span class="sxs-lookup"><span data-stu-id="b51dc-118">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="b51dc-119">In de **bestemming** sectie kiezen **Selecteer een virtuele machine** en kies de juiste virtuele machine en poort om te testen.</span><span class="sxs-lookup"><span data-stu-id="b51dc-119">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="b51dc-120">Nadat u op **controleren**, de verbinding tussen de virtuele machines op de opgegeven poort worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="b51dc-120">Once you click **Check**, the connectivity between the virtual machines on the port specified are checked.</span></span> <span data-ttu-id="b51dc-121">De doel-virtuele machine is niet bereikbaar, een overzicht van hops weergegeven in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b51dc-121">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![Resultaten van de verbinding voor een virtuele machine][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="b51dc-123">Controleer de verbindingen van het externe eindpunt</span><span class="sxs-lookup"><span data-stu-id="b51dc-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="b51dc-124">Als u wilt controleren de connectiviteit en de latentie van een extern eindpunt, kies de **handmatig opgeven** keuzerondje in de **bestemming** sectie, voert u de url en de poort en klik op **controleren**.</span><span class="sxs-lookup"><span data-stu-id="b51dc-124">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="b51dc-125">Dit wordt gebruikt voor externe eindpunten zoals websites en -opslag-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="b51dc-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Resultaten van de verbinding voor een website][2]

## <a name="next-steps"></a><span data-ttu-id="b51dc-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b51dc-127">Next steps</span></span>

<span data-ttu-id="b51dc-128">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b51dc-128">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b51dc-129">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b51dc-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
