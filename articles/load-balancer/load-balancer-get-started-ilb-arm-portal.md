---
title: een interne load balancer - Azure-portal aaaCreate | Microsoft Docs
description: Meer informatie over hoe de toocreate een interne load balancer in Resource Manager, met behulp van hello Azure-portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="b3ed1-103">Maken van een interne load balancer in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b3ed1-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3ed1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3ed1-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="b3ed1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3ed1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="b3ed1-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b3ed1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="b3ed1-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="b3ed1-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b3ed1-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b3ed1-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b3ed1-109">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b3ed1-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="b3ed1-110">Aan de slag met het maken van een interne load balancer met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3ed1-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="b3ed1-111">Hallo volgende stappen toocreate een interne load balancer uit hello Azure Portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="b3ed1-112">Open een browser en ga toohello [Azure-portal](http://portal.azure.com), en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="b3ed1-113">In Hallo bovenste linkerzijde van Hallo scherm, klikt u op **nieuw** > **Networking** > **Load balancer**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="b3ed1-114">In Hallo **maken load balancer** blade, voer een **naam** voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="b3ed1-115">Klik onder **Schema** op **Intern**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="b3ed1-116">Klik op **virtueel netwerk**, en vervolgens selecteert Hallo virtueel netwerk waar u toocreate Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b3ed1-117">Als u Hallo virtueel netwerk die u wilt dat toouse niet ziet, controleert u Hallo **locatie** u gebruikt voor Hallo load balancer en dienovereenkomstig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="b3ed1-118">Klik op **Subnet**, en selecteer vervolgens Hallo subnet waar u toocreate Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="b3ed1-119">Onder **IP-adrestoewijzing**, klikt u op **dynamische** of **statische**, afhankelijk van of u Hallo IP-adres wilt voor Hallo load balancer toobe vaste (statische) of niet.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b3ed1-120">Als u een statisch IP-adres toouse selecteert, hebt u tooprovide een adres voor Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="b3ed1-121">Onder **resourcegroep** Geef Hallo-naam van een nieuwe resourcegroep voor Hallo load balancer, of klik op **Selecteer een bestaande** en selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="b3ed1-122">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="b3ed1-123">Taakverdelingsregels configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-123">Configure load balancing rules</span></span>

<span data-ttu-id="b3ed1-124">Na het Hallo load balancer maken, gaat u toohello load balancer resource tooconfigure deze.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="b3ed1-125">U moet tooconfigure eerst een back-end-adresgroep en een test voordat u een load-balancingregel configureert.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="b3ed1-126">Stap 1: Een back-endgroep configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="b3ed1-127">Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b3ed1-128">In Hallo **instellingen** blade, klikt u op **back-endpools**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="b3ed1-129">In Hallo **back-end-adresgroepen** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="b3ed1-130">In Hallo **back-endpool toevoegen** blade, voer een **naam** voor Hallo back-endpool en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="b3ed1-131">Stap 2: Een test configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="b3ed1-132">Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b3ed1-133">In Hallo **instellingen** blade, klikt u op **tests**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="b3ed1-134">In Hallo **Probes** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="b3ed1-135">In Hallo **toevoegen test** blade, voer een **naam** voor de test Hallo.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="b3ed1-136">Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).</span><span class="sxs-lookup"><span data-stu-id="b3ed1-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="b3ed1-137">Onder **poort**, Hallo poort toouse opgeven bij het openen van Hallo test.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="b3ed1-138">Onder **pad** (voor HTTP-tests alleen) Hallo pad toouse als een test opgeven.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="b3ed1-139">Onder **Interval** opgeven hoe vaak tooprobe toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="b3ed1-140">Onder **drempelwaarde voor onjuiste status**, geef het aantal pogingen moeten worden gemist voordat Hallo back-end virtuele machine is als beschadigd gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="b3ed1-141">Klik op **OK** toocreate test.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="b3ed1-142">Stap 3: Taakverdelingsregels configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="b3ed1-143">Klik in hello Azure-portal, op **Bladeren** > **Taakverdelers**, en klik vervolgens op Hallo load balancer die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b3ed1-144">In Hallo **instellingen** blade, klikt u op **Taakverdelingsregels**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="b3ed1-145">In Hallo **Taakverdelingsregels** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="b3ed1-146">In Hallo **toevoegen taakverdelingsregel** blade, voer een **naam** voor Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="b3ed1-147">Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).</span><span class="sxs-lookup"><span data-stu-id="b3ed1-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="b3ed1-148">Onder **poort**, opgeven Hallo poort clients verbinding tooin Hallo load balancer.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="b3ed1-149">Onder **backendpoort**, Hallo poort toobe gebruikt in de back-endpool Hallo opgeven (meestal Hallo load balancer-poort en back-endpoort Hallo zijn Hallo dezelfde).</span><span class="sxs-lookup"><span data-stu-id="b3ed1-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="b3ed1-150">Onder **back-endpool**, selecteer Hallo back-end-groep u die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="b3ed1-151">Onder **sessiepersistentie**, selecteer de manier waarop u wilt dat toopersist sessies.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="b3ed1-152">Onder **time-out voor inactiviteit (minuten)**, time-out voor inactiviteit van Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="b3ed1-153">Klik onder **Zwevend IP (Direct Server Return)** op **Uitgeschakeld** of **Ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="b3ed1-154">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3ed1-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3ed1-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3ed1-155">Next steps</span></span>

[<span data-ttu-id="b3ed1-156">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b3ed1-157">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="b3ed1-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

