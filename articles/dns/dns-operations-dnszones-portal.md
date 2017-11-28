---
title: aaaManage DNS-zones in Azure DNS - Azure-portal | Microsoft Docs
description: U kunt DNS-zones met hello Azure-portal beheren. Dit artikel wordt beschreven hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="2e5ab-104">Hoe toomanage DNS-Zones in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2e5ab-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e5ab-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2e5ab-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="2e5ab-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e5ab-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="2e5ab-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2e5ab-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="2e5ab-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2e5ab-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="2e5ab-109">Dit artikel laat zien hoe toomanage uw DNS-zones met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="2e5ab-110">U kunt ook de DNS-zones met behulp van de platformoverschrijdende Hallo beheren [Azure CLI](dns-operations-dnszones-cli.md) of hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="2e5ab-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="2e5ab-111">Een DNS-zone maken</span><span class="sxs-lookup"><span data-stu-id="2e5ab-111">Create a DNS zone</span></span>

1. <span data-ttu-id="2e5ab-112">Meld u aan toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2e5ab-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="2e5ab-113">Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS-zone](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="2e5ab-115">Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:</span><span class="sxs-lookup"><span data-stu-id="2e5ab-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="2e5ab-116">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-116">**Setting**</span></span> | <span data-ttu-id="2e5ab-117">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-117">**Value**</span></span> | <span data-ttu-id="2e5ab-118">**Details**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="2e5ab-119">**Naam**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-119">**Name**</span></span>|<span data-ttu-id="2e5ab-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="2e5ab-120">contoso.com</span></span>|<span data-ttu-id="2e5ab-121">Hallo-naam van Hallo DNS-zone</span><span class="sxs-lookup"><span data-stu-id="2e5ab-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="2e5ab-122">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-122">**Subscription**</span></span>|<span data-ttu-id="2e5ab-123">[Uw abonnement]</span><span class="sxs-lookup"><span data-stu-id="2e5ab-123">[Your subscription]</span></span>|<span data-ttu-id="2e5ab-124">Selecteer een abonnement toocreate Hallo DNS-zone in.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="2e5ab-125">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-125">**Resource group**</span></span>|<span data-ttu-id="2e5ab-126">**Nieuwe maken:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="2e5ab-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="2e5ab-127">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-127">Create a resource group.</span></span> <span data-ttu-id="2e5ab-128">de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="2e5ab-129">meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="2e5ab-130">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="2e5ab-130">**Location**</span></span>|<span data-ttu-id="2e5ab-131">VS - west</span><span class="sxs-lookup"><span data-stu-id="2e5ab-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="2e5ab-132">Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="2e5ab-133">Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="2e5ab-134">Lijst met DNS-zones</span><span class="sxs-lookup"><span data-stu-id="2e5ab-134">List DNS zones</span></span>

<span data-ttu-id="2e5ab-135">In Azure-portal Hallo, te navigeren**meer services** > **Networking** > **DNS-zones**.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="2e5ab-136">Elke DNS-zone, is het eigen resource, zoals het aantal recordsets en naamservers kunnen worden bekeken in deze weergave.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="2e5ab-137">Hallo kolom **NAAMSERVERS** is niet in de standaardweergave hello, tooadd Klik **kolommen**, selecteer **naamservers** en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![aanbieding DNS-zones](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="2e5ab-139">Een DNS-zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="2e5ab-139">Delete a DNS zone</span></span>

<span data-ttu-id="2e5ab-140">Navigeer tooa DNS-zone in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="2e5ab-141">Op Hallo **DNS-zone** blade, klikt u op **zone verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="2e5ab-142">U bent na vragen aan gebruiker tooconfirm u toodelete Hallo DNS-zone zijn productiviteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="2e5ab-143">Een DNS-zone verwijderen, verwijdert tevens alle Hallo-records die zijn opgenomen in het Hallo-zone.</span><span class="sxs-lookup"><span data-stu-id="2e5ab-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e5ab-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e5ab-144">Next steps</span></span>

<span data-ttu-id="2e5ab-145">Meer informatie over hoe toowork met uw DNS-Zone en records in via [aan de slag met Azure DNS hello Azure-portal met](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e5ab-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
