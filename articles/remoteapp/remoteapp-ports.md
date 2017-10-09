---
title: "aaaList van toowhitelist poorten en URL's voor Azure RemoteApp geïmplementeerd in het virtuele netwerk van de klant | Microsoft Docs"
description: Informatie over welke poorten en URL's moet u tooconfigure voor communicatie via Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="3e955-103">Lijst met URL's en poorten toopermit toegang voor Azure RemoteApp geïmplementeerd in klant virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="3e955-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3e955-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="3e955-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3e955-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3e955-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3e955-106">Als u een Azure RemoteApp-cloud of hybride verzameling in een virtueel netwerk (VNET) implementeert, bekijk Hallo poortinformatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="3e955-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="3e955-107">Lees voor meer informatie over virtuele netwerken [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e955-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="3e955-108">Als u een netwerkbeveiligingsgroep (NSG) beperken verkeer toohello virtueel netwerkresources in uw verzameling hebt gemaakt, zorg er dan voor dat Hallo volgende poorten zijn toegankelijk is en is toegestaan via Hallo beveiligingsbeleid op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3e955-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="3e955-109">Lees voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep? (NSG) ](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3e955-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="3e955-110">Azure RemoteApp-subnet moet toegang toothese eindpunten en URL's:</span><span class="sxs-lookup"><span data-stu-id="3e955-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="3e955-111">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3e955-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="3e955-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="3e955-112">*.servicebus.net</span></span>
* <span data-ttu-id="3e955-113">https://*.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3e955-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3e955-114">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3e955-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="3e955-115">https://*RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3e955-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3e955-116">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="3e955-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="3e955-117">Uitgaand: TCP: TCP: 443, 9351, 9352, 10101 10175</span><span class="sxs-lookup"><span data-stu-id="3e955-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="3e955-118">Optioneel – UDP: 10201 10275</span><span class="sxs-lookup"><span data-stu-id="3e955-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="3e955-119">Azure RemoteApp-clients moeten toegang tot toothese eindpunten en URL's:</span><span class="sxs-lookup"><span data-stu-id="3e955-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="3e955-120">Door clients heb Hallo desktops, apparaten enzovoort die mensen die gebruik tooconnect toohello apps geïmplementeerd in hello Azure RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="3e955-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="3e955-121">https://telemetry.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3e955-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="3e955-122">https://*.RemoteApp.windowsazure.com (Hallo optionele UDP-poorten zijn voor dit adres)</span><span class="sxs-lookup"><span data-stu-id="3e955-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="3e955-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3e955-123">https://login.windows.net</span></span>  
* <span data-ttu-id="3e955-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3e955-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="3e955-125">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="3e955-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="3e955-126">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="3e955-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="3e955-127">Uitgaand: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="3e955-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="3e955-128">Optionele - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="3e955-128">Optional - UDP: 3391</span></span> 

