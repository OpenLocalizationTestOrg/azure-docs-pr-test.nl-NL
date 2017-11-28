---
title: aaaCannot verwijdert een virtueel netwerk in Azure | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Hallo probleem waarin u een virtueel netwerk in Azure niet verwijderen.
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="33cde-103">Voor probleemoplossing: Een virtueel netwerk in Azure toodelete mislukt</span><span class="sxs-lookup"><span data-stu-id="33cde-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="33cde-104">Fouten kan worden weergegeven wanneer u toodelete een virtueel netwerk in Microsoft Azure probeert.</span><span class="sxs-lookup"><span data-stu-id="33cde-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="33cde-105">In dit artikel voor probleemoplossing stappen toohelp vindt u dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="33cde-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="33cde-106">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="33cde-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="33cde-107">[Controleer of een virtuele netwerkgateway actief is in het virtuele netwerk Hallo](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="33cde-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="33cde-108">[Controleer of een application gateway actief is in het virtuele netwerk Hallo](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="33cde-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="33cde-109">[Controleer of de Azure Active Directory Domain Services is ingeschakeld in het virtuele netwerk Hallo](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="33cde-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="33cde-110">[Controleer of Hallo virtueel netwerk verbonden tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="33cde-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="33cde-111">[Controleer of een virtuele machine nog steeds actief is in het virtuele netwerk Hallo](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="33cde-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="33cde-112">[Controleer of het virtuele netwerk Hallo is vastgelopen bij migratie](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="33cde-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="33cde-113">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="33cde-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="33cde-114">Controleer of een virtuele netwerkgateway actief is in het virtuele netwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="33cde-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="33cde-115">tooremove hello virtueel netwerk, moet u eerst de virtuele netwerkgateway Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33cde-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="33cde-116">Ga voor klassieke virtuele netwerken toohello **overzicht** pagina van Hallo klassiek virtueel netwerk in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="33cde-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="33cde-117">In Hallo **VPN-verbindingen** sectie, als Hallo gateway wordt uitgevoerd in het virtuele netwerk hello, ziet u Hallo IP-adres van het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="33cde-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Controleer of de gateway is actief](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="33cde-119">Ga voor virtuele netwerken, toohello **overzicht** pagina van het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="33cde-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="33cde-120">Controleer **verbonden apparaten** voor de virtuele netwerkgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="33cde-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Hallo aangesloten apparaat controleren](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="33cde-122">Voordat u Hallo gateway verwijderen kunt, eerste Verwijder een **verbinding** objecten in het Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="33cde-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="33cde-123">Controleer of een application gateway actief is in het virtuele netwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="33cde-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="33cde-124">Ga toohello **overzicht** pagina van het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="33cde-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="33cde-125">Controleer de Hallo **verbonden apparaten** voor Hallo application gateway.</span><span class="sxs-lookup"><span data-stu-id="33cde-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Hallo aangesloten apparaat controleren](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="33cde-127">Als er een application gateway, moet u deze verwijderen voordat u het virtuele netwerk Hallo kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33cde-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="33cde-128">Controleer of de Azure Active Directory Domain Services is ingeschakeld in het virtuele netwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="33cde-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="33cde-129">Als Hallo Active Directory Domain Services ingeschakeld en verbonden toohello virtueel netwerk is, kunt u dit virtuele netwerk niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33cde-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Hallo aangesloten apparaat controleren](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="33cde-131">toodisable Hallo service, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="33cde-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="33cde-132">Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="33cde-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="33cde-133">Selecteer in het linkerdeelvenster Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33cde-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="33cde-134">Selecteer hello Azure Active Directory (Azure AD) directory met Active Directory Domain Services is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="33cde-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="33cde-135">Selecteer Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="33cde-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="33cde-136">Onder **domeinservices**, Hallo wijzigen **domeinservices inschakelen voor deze map** te optie**Nee**.</span><span class="sxs-lookup"><span data-stu-id="33cde-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="33cde-137">Controleer of Hallo virtueel netwerk verbonden tooother resource</span><span class="sxs-lookup"><span data-stu-id="33cde-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="33cde-138">Controleren op Circuitkoppelingen, verbindingen en virtuele netwerk peerings.</span><span class="sxs-lookup"><span data-stu-id="33cde-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="33cde-139">Elk van deze waarden kan een virtueel netwerk verwijdering toofail veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="33cde-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="33cde-140">Hallo is aanbevolen verwijdering volgorde als volgt:</span><span class="sxs-lookup"><span data-stu-id="33cde-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="33cde-141">Gatewayverbindingen</span><span class="sxs-lookup"><span data-stu-id="33cde-141">Gateway connections</span></span>
2. <span data-ttu-id="33cde-142">Gateways</span><span class="sxs-lookup"><span data-stu-id="33cde-142">Gateways</span></span>
3. <span data-ttu-id="33cde-143">IP-adressen</span><span class="sxs-lookup"><span data-stu-id="33cde-143">IPs</span></span>
4. <span data-ttu-id="33cde-144">Virtueel netwerk peerings</span><span class="sxs-lookup"><span data-stu-id="33cde-144">Virtual network peerings</span></span>
5. <span data-ttu-id="33cde-145">App Service-omgeving (as-omgeving)</span><span class="sxs-lookup"><span data-stu-id="33cde-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="33cde-146">Controleer of een virtuele machine nog steeds actief is in het virtuele netwerk Hallo</span><span class="sxs-lookup"><span data-stu-id="33cde-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="33cde-147">Zorg ervoor dat er geen virtuele machine in het virtuele netwerk Hallo is.</span><span class="sxs-lookup"><span data-stu-id="33cde-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="33cde-148">Controleer of het virtuele netwerk Hallo is vastgelopen bij migratie</span><span class="sxs-lookup"><span data-stu-id="33cde-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="33cde-149">Als het virtuele netwerk Hallo is vastgelopen in de migratiestatus van een, kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="33cde-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="33cde-150">Hallo na de opdracht tooabort Hallo migratie uitvoeren en verwijder vervolgens Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="33cde-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="33cde-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33cde-151">Next steps</span></span>

- [<span data-ttu-id="33cde-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="33cde-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="33cde-153">Veelgestelde vragen over virtuele Azure-netwerken (FAQ)</span><span class="sxs-lookup"><span data-stu-id="33cde-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)