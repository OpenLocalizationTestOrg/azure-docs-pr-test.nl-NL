---
title: "Lijst met poorten en URL's voor goedgekeurde IP-adressen voor Azure RemoteApp geïmplementeerd in het virtuele netwerk van de klant | Microsoft Docs"
description: Meer informatie over welke poorten en URL's u wilt configureren voor communicatie via Azure RemoteApp.
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
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="c2b64-103">Lijst met poorten en URL's om toegang te verlenen voor Azure RemoteApp geïmplementeerd in klant virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="c2b64-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c2b64-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="c2b64-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c2b64-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c2b64-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c2b64-106">Als u een Azure RemoteApp-cloud of hybride verzameling in een virtueel netwerk (VNET) implementeert, raadpleegt u de volgende poortinformatie.</span><span class="sxs-lookup"><span data-stu-id="c2b64-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="c2b64-107">Lees voor meer informatie over virtuele netwerken [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2b64-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="c2b64-108">Als u verkeer beperkt tot de resources van het virtuele netwerk in uw verzameling een netwerkbeveiligingsgroep (NSG) hebt gemaakt, zorg er dan voor dat de volgende poorten zijn toegankelijk is en is toegestaan door het beveiligingsbeleid op het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="c2b64-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="c2b64-109">Lees voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep? (NSG) ](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c2b64-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="c2b64-110">Azure RemoteApp-subnet moet toegang tot deze eindpunten en URL's:</span><span class="sxs-lookup"><span data-stu-id="c2b64-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="c2b64-111">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="c2b64-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="c2b64-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="c2b64-112">*.servicebus.net</span></span>
* <span data-ttu-id="c2b64-113">https://*.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="c2b64-114">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="c2b64-115">https://*RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="c2b64-116">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="c2b64-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="c2b64-117">Uitgaand: TCP: TCP: 443, 9351, 9352, 10101 10175</span><span class="sxs-lookup"><span data-stu-id="c2b64-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="c2b64-118">Optioneel – UDP: 10201 10275</span><span class="sxs-lookup"><span data-stu-id="c2b64-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="c2b64-119">Azure RemoteApp-clients moeten toegang tot deze eindpunten en URL's:</span><span class="sxs-lookup"><span data-stu-id="c2b64-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="c2b64-120">Door clients dat ik de desktops, enzovoort. die mensen gebruiken om de apps die worden geïmplementeerd in de Azure RemoteApp-verzameling met apparaten.</span><span class="sxs-lookup"><span data-stu-id="c2b64-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="c2b64-121">https://telemetry.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="c2b64-122">https://*.RemoteApp.windowsazure.com (de optionele UDP-poorten zijn voor dit adres)</span><span class="sxs-lookup"><span data-stu-id="c2b64-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="c2b64-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="c2b64-123">https://login.windows.net</span></span>  
* <span data-ttu-id="c2b64-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="c2b64-125">https://www.RemoteApp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="c2b64-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="c2b64-126">https://*.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="c2b64-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="c2b64-127">Uitgaand: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="c2b64-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="c2b64-128">Optionele - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="c2b64-128">Optional - UDP: 3391</span></span> 

