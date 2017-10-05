---
title: Een interne load balancer maken in Azure Portal | Microsoft Docs
description: Meer informatie over hoe u met Azure Portal een interne load balancer maakt in Resource Manager
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
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="baae5-103">Een interne load balancer maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="baae5-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="baae5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="baae5-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="baae5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="baae5-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="baae5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="baae5-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="baae5-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="baae5-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="baae5-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="baae5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="baae5-109">Dit artikel bevat informatie over het Resource Manager-implementatiemodel, dat door Microsoft wordt aanbevolen voor de meeste nieuwe implementaties in plaats van het [klassieke implementatiemodel](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="baae5-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="baae5-110">Aan de slag met het maken van een interne load balancer met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="baae5-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="baae5-111">Gebruik de volgende stappen om een interne load balancer te maken vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="baae5-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="baae5-112">Open een browser, ga naar [Azure Portal](http://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="baae5-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="baae5-113">Klik linksboven in het scherm op **Nieuw** > **Netwerken** > **Load balancer**.</span><span class="sxs-lookup"><span data-stu-id="baae5-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="baae5-114">Voer op de blade **Load balancer maken** een **naam** in voor de load balancer.</span><span class="sxs-lookup"><span data-stu-id="baae5-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="baae5-115">Klik onder **Schema** op **Intern**.</span><span class="sxs-lookup"><span data-stu-id="baae5-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="baae5-116">Klik op **Virtueel netwerk** en selecteer het virtuele netwerk waarin u de load balancer wilt maken.</span><span class="sxs-lookup"><span data-stu-id="baae5-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="baae5-117">Als u het te gebruiken virtuele netwerk niet ziet, controleert u de **locatie** van de load balancer en past u deze dienovereenkomstig aan.</span><span class="sxs-lookup"><span data-stu-id="baae5-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="baae5-118">Klik op **Subnet** en selecteer het subnet waarin u de load balancer wilt maken.</span><span class="sxs-lookup"><span data-stu-id="baae5-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="baae5-119">Klik onder **IP-adrestoewijzing** op **Dynamisch** of **Statisch**, afhankelijk van of u een vast (statisch) IP-adres voor de load balancer wilt of niet.</span><span class="sxs-lookup"><span data-stu-id="baae5-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="baae5-120">Als u voor het gebruik van een statisch IP-adres kiest, moet u een adres voor de load balancer opgeven.</span><span class="sxs-lookup"><span data-stu-id="baae5-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="baae5-121">Geef onder **Resourcegroep** de naam op van een nieuwe resourcegroep voor de load balancer of klik op **Bestaande selecteren** en selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="baae5-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="baae5-122">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="baae5-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="baae5-123">Taakverdelingsregels configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-123">Configure load balancing rules</span></span>

<span data-ttu-id="baae5-124">Wanneer de load balancer is gemaakt, navigeert u naar de resource van de load balancer om deze te configureren.</span><span class="sxs-lookup"><span data-stu-id="baae5-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="baae5-125">U moet eerst een back-endadresgroep en een test configureren voordat u een taakverdelingsregel configureert.</span><span class="sxs-lookup"><span data-stu-id="baae5-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="baae5-126">Stap 1: Een back-endgroep configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="baae5-127">Klik in Azure Portal op **Bladeren** > **Load balancers** en vervolgens op de load balancer die u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="baae5-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="baae5-128">Klik op de blade **Instellingen** op **Back-endgroepen**.</span><span class="sxs-lookup"><span data-stu-id="baae5-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="baae5-129">Klik op de blade **Back-endadresgroepen** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="baae5-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="baae5-130">Voer op de blade **Back-endgroep toevoegen** een **Naam** in voor de back-endgroep en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="baae5-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="baae5-131">Stap 2: Een test configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="baae5-132">Klik in Azure Portal op **Bladeren** > **Load balancers** en vervolgens op de load balancer die u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="baae5-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="baae5-133">Klik op de blade **Instellingen** op **Tests**.</span><span class="sxs-lookup"><span data-stu-id="baae5-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="baae5-134">Klik op de blade **Tests** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="baae5-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="baae5-135">Voer op de blade **Test toevoegen** een **Naam** in voor de test.</span><span class="sxs-lookup"><span data-stu-id="baae5-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="baae5-136">Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).</span><span class="sxs-lookup"><span data-stu-id="baae5-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="baae5-137">Geef onder **Poort** op welke poort u voor de test wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="baae5-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="baae5-138">Geef onder **Pad** (alleen voor HTTP-tests) het pad op dat u voor de test wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="baae5-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="baae5-139">Geef onder **Interval** op hoe vaak u de toepassing wilt testen.</span><span class="sxs-lookup"><span data-stu-id="baae5-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="baae5-140">Geef onder **Drempelwaarde voor onjuiste status** op hoeveel pogingen er moeten mislukken voordat de virtuele back-endmachine wordt aangeduid als Niet in orde.</span><span class="sxs-lookup"><span data-stu-id="baae5-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="baae5-141">Klik op **OK** om de test te maken.</span><span class="sxs-lookup"><span data-stu-id="baae5-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="baae5-142">Stap 3: Taakverdelingsregels configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="baae5-143">Klik in Azure Portal op **Bladeren** > **Load balancers** en vervolgens op de load balancer die u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="baae5-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="baae5-144">Klik op de blade **Instellingen** op **Taakverdelingsregels**.</span><span class="sxs-lookup"><span data-stu-id="baae5-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="baae5-145">Klik op de blade **Taakverdelingsregels** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="baae5-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="baae5-146">Voer op de blade **Taakverdelingsregel toevoegen** een **Naam** in voor de regel.</span><span class="sxs-lookup"><span data-stu-id="baae5-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="baae5-147">Selecteer onder **Protocol** **HTTP** (voor websites) of **TCP** (voor andere TCP-toepassingen).</span><span class="sxs-lookup"><span data-stu-id="baae5-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="baae5-148">Geef onder **Poort** op via welke poort clients verbinding maken met de load balancer.</span><span class="sxs-lookup"><span data-stu-id="baae5-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="baae5-149">Geef onder **Back-endpoort** de poort op die in de back-endgroep moet worden gebruikt (gewoonlijk zijn de load balancer-poort en de back-endpoort hetzelfde).</span><span class="sxs-lookup"><span data-stu-id="baae5-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="baae5-150">Selecteer onder **Back-endgroep** de back-endgroep die u hierboven hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="baae5-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="baae5-151">Selecteer onder **Sessiepersistentie** hoe sessies moeten worden standgehouden.</span><span class="sxs-lookup"><span data-stu-id="baae5-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="baae5-152">Geef onder **Time-out voor inactiviteit (minuten)** de time-out voor inactiviteit op.</span><span class="sxs-lookup"><span data-stu-id="baae5-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="baae5-153">Klik onder **Zwevend IP (Direct Server Return)** op **Uitgeschakeld** of **Ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="baae5-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="baae5-154">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="baae5-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="baae5-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="baae5-155">Next steps</span></span>

[<span data-ttu-id="baae5-156">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="baae5-157">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="baae5-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

