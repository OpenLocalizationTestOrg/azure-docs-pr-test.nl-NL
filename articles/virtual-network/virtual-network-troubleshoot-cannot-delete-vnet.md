---
title: Een virtueel netwerk in Azure niet verwijderen | Microsoft Docs
description: Informatie over het oplossen van het probleem waarin u een virtueel netwerk in Azure niet verwijderen.
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
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="371d9-103">Voor probleemoplossing: Kan niet verwijderen van een virtueel netwerk in Azure</span><span class="sxs-lookup"><span data-stu-id="371d9-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="371d9-104">Fouten kan worden weergegeven wanneer u probeert te verwijderen van een virtueel netwerk in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="371d9-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="371d9-105">Dit artikel bevat de stappen voor probleemoplossing waarmee u kunt dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="371d9-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="371d9-106">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="371d9-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="371d9-107">[Controleer of een virtuele netwerkgateway actief is in het virtuele netwerk](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="371d9-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="371d9-108">[Controleer of een application gateway actief is in het virtuele netwerk](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="371d9-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="371d9-109">[Controleer of de Azure Active Directory Domain Services is ingeschakeld in het virtuele netwerk](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="371d9-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="371d9-110">[Controleer of het virtuele netwerk is verbonden met andere resources](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="371d9-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="371d9-111">[Controleer of een virtuele machine nog steeds actief is in het virtuele netwerk](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="371d9-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="371d9-112">[Controleer of het virtuele netwerk is vastgelopen bij migratie](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="371d9-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="371d9-113">Stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="371d9-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="371d9-114">Controleer of een virtuele netwerkgateway actief is in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="371d9-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="371d9-115">Als u wilt verwijderen van het virtuele netwerk, moet u eerst de virtuele netwerkgateway verwijderen.</span><span class="sxs-lookup"><span data-stu-id="371d9-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="371d9-116">Voor klassieke virtuele netwerken, gaat u naar de **overzicht** pagina van het klassieke virtuele netwerk in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="371d9-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="371d9-117">In de **VPN-verbindingen** sectie, als de gateway wordt uitgevoerd in het virtuele netwerk, ziet u het IP-adres van de gateway.</span><span class="sxs-lookup"><span data-stu-id="371d9-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Controleer of de gateway is actief](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="371d9-119">Voor virtuele netwerken, gaat u naar de **overzicht** pagina van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="371d9-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="371d9-120">Controleer **verbonden apparaten** voor de virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="371d9-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Controleer het aangesloten apparaat](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="371d9-122">Voordat u de gateway verwijderen kunt, eerste Verwijder een **verbinding** objecten in de gateway.</span><span class="sxs-lookup"><span data-stu-id="371d9-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="371d9-123">Controleer of een application gateway actief is in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="371d9-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="371d9-124">Ga naar de **overzicht** pagina van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="371d9-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="371d9-125">Controleer de **verbonden apparaten** voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="371d9-125">Check the **Connected devices** for the application gateway.</span></span>

![Controleer het aangesloten apparaat](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="371d9-127">Als er een application gateway, moet u deze verwijderen voordat u het virtuele netwerk kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="371d9-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="371d9-128">Controleer of de Azure Active Directory Domain Services is ingeschakeld in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="371d9-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="371d9-129">Als de Active Directory Domain Services is ingeschakeld en met het virtuele netwerk verbonden, kunt u dit virtuele netwerk niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="371d9-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Controleer het aangesloten apparaat](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="371d9-131">Schakel de service de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="371d9-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="371d9-132">Ga naar de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="371d9-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="371d9-133">Selecteer in het linkerdeelvenster **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="371d9-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="371d9-134">Selecteer de map voor Azure Active Directory (Azure AD) met Active Directory Domain Services is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="371d9-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="371d9-135">Selecteer de tab **Configureren**.</span><span class="sxs-lookup"><span data-stu-id="371d9-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="371d9-136">Onder **domeinservices**, wijzig de **domeinservices inschakelen voor deze map** optie naar **Nee**.</span><span class="sxs-lookup"><span data-stu-id="371d9-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="371d9-137">Controleer of het virtuele netwerk is verbonden met andere resources</span><span class="sxs-lookup"><span data-stu-id="371d9-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="371d9-138">Controleren op Circuitkoppelingen, verbindingen en virtuele netwerk peerings.</span><span class="sxs-lookup"><span data-stu-id="371d9-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="371d9-139">Deze kan leiden tot een virtueel netwerk verwijderen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="371d9-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="371d9-140">De volgorde van de aanbevolen verwijdering is als volgt:</span><span class="sxs-lookup"><span data-stu-id="371d9-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="371d9-141">Gatewayverbindingen</span><span class="sxs-lookup"><span data-stu-id="371d9-141">Gateway connections</span></span>
2. <span data-ttu-id="371d9-142">Gateways</span><span class="sxs-lookup"><span data-stu-id="371d9-142">Gateways</span></span>
3. <span data-ttu-id="371d9-143">IP-adressen</span><span class="sxs-lookup"><span data-stu-id="371d9-143">IPs</span></span>
4. <span data-ttu-id="371d9-144">Virtueel netwerk peerings</span><span class="sxs-lookup"><span data-stu-id="371d9-144">Virtual network peerings</span></span>
5. <span data-ttu-id="371d9-145">App Service-omgeving (as-omgeving)</span><span class="sxs-lookup"><span data-stu-id="371d9-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="371d9-146">Controleer of een virtuele machine nog steeds actief is in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="371d9-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="371d9-147">Zorg ervoor dat er geen virtuele machine zich in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="371d9-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="371d9-148">Controleer of het virtuele netwerk is vastgelopen bij migratie</span><span class="sxs-lookup"><span data-stu-id="371d9-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="371d9-149">Als het virtuele netwerk is vastgelopen in de migratiestatus van een, kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="371d9-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="371d9-150">Voer de volgende opdracht om af te breken van de migratie en verwijder vervolgens het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="371d9-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="371d9-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="371d9-151">Next steps</span></span>

- [<span data-ttu-id="371d9-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="371d9-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="371d9-153">Veelgestelde vragen over virtuele Azure-netwerken (FAQ)</span><span class="sxs-lookup"><span data-stu-id="371d9-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)