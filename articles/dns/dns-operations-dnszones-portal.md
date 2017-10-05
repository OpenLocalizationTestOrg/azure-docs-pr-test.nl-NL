---
title: DNS-zones in Azure DNS - Azure-portal beheren | Microsoft Docs
description: U kunt DNS-zones met de Azure portal beheren. Dit artikel wordt beschreven hoe u bijwerken, verwijderen en DNS-zones maken op Azure DNS
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="2cbe0-104">DNS-Zones beheren in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="2cbe0-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cbe0-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2cbe0-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="2cbe0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cbe0-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="2cbe0-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2cbe0-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="2cbe0-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2cbe0-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="2cbe0-109">In dit artikel laat zien hoe uw DNS-zones beheren met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="2cbe0-110">U kunt ook de DNS-zones met behulp van de platformoverschrijdende beheren [Azure CLI](dns-operations-dnszones-cli.md) of de Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="2cbe0-111">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="2cbe0-111">Create a DNS zone</span></span>

1. <span data-ttu-id="2cbe0-112">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2cbe0-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="2cbe0-113">Klik in het menu Hub en klik op **Nieuw > Netwerken >** en klik vervolgens op **DNS-zone** om de blade DNS-zone maken te openen.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS-zone](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="2cbe0-115">Voer op de blade **DNS-zone maken** de volgende waarden in en klik op **Maken**:</span><span class="sxs-lookup"><span data-stu-id="2cbe0-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="2cbe0-116">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-116">**Setting**</span></span> | <span data-ttu-id="2cbe0-117">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-117">**Value**</span></span> | <span data-ttu-id="2cbe0-118">**Details**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="2cbe0-119">**Naam**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-119">**Name**</span></span>|<span data-ttu-id="2cbe0-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="2cbe0-120">contoso.com</span></span>|<span data-ttu-id="2cbe0-121">De naam van de DNS-zone</span><span class="sxs-lookup"><span data-stu-id="2cbe0-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="2cbe0-122">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-122">**Subscription**</span></span>|<span data-ttu-id="2cbe0-123">[Uw abonnement]</span><span class="sxs-lookup"><span data-stu-id="2cbe0-123">[Your subscription]</span></span>|<span data-ttu-id="2cbe0-124">Selecteer een abonnement waarin de DNS-zone moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="2cbe0-125">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-125">**Resource group**</span></span>|<span data-ttu-id="2cbe0-126">**Nieuwe maken:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="2cbe0-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="2cbe0-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-127">Create a resource group.</span></span> <span data-ttu-id="2cbe0-128">De naam van de resourcegroep moet uniek zijn binnen het abonnement dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="2cbe0-129">Lees het overzichtsartikel over [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="2cbe0-130">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="2cbe0-130">**Location**</span></span>|<span data-ttu-id="2cbe0-131">VS - west</span><span class="sxs-lookup"><span data-stu-id="2cbe0-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="2cbe0-132">De resourcegroep verwijst naar de locatie van de resourcegroep en heeft geen invloed op de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="2cbe0-133">De locatie van de DNS-zone is altijd 'global' en wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="2cbe0-134">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="2cbe0-134">List DNS zones</span></span>

<span data-ttu-id="2cbe0-135">Navigeer in de Azure-portal naar **meer services** > **Networking** > **DNS-zones**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="2cbe0-136">Elke DNS-zone, is het eigen resource, zoals het aantal recordsets en naamservers kunnen worden bekeken in deze weergave.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="2cbe0-137">De kolom **NAAMSERVERS** bevindt zich niet in de standaardweergave toe te voegen klikt u op **kolommen**, selecteer **naamservers** en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![aanbieding DNS-zones](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="2cbe0-139">Een DNS-zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="2cbe0-139">Delete a DNS zone</span></span>

<span data-ttu-id="2cbe0-140">Navigeer naar een DNS-zone in de portal.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="2cbe0-141">Op de **DNS-zone** blade, klikt u op **zone verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="2cbe0-142">U wordt gevraagd om te bevestigen dat u willen verwijderen van de DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="2cbe0-143">Een DNS-zone verwijderen, verwijdert tevens alle records die zijn opgenomen in de zone.</span><span class="sxs-lookup"><span data-stu-id="2cbe0-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cbe0-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2cbe0-144">Next steps</span></span>

<span data-ttu-id="2cbe0-145">Meer informatie over het werken met uw DNS-Zone en records in via [aan de slag met Azure DNS met Azure portal](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cbe0-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>