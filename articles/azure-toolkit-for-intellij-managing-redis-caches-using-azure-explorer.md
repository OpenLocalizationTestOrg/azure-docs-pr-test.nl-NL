---
title: Azure Explorer aaaManaging met behulp van Redis-Caches Hallo voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toomanage uw Azure redis cache met behulp van hello Azure Explorer voor IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="93485-103">Beheren van Redis-Caches hello Azure Explorer voor IntelliJ gebruiken</span><span class="sxs-lookup"><span data-stu-id="93485-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="93485-104">Hello Azure Explorer, die deel uitmaakt van hello Azure Toolkit voor IntelliJ, Java-ontwikkelaars met een eenvoudig-en-klare oplossing voor het beheren van redis-caches in de Azure-account uit binnen Hallo IntelliJ IDE biedt.</span><span class="sxs-lookup"><span data-stu-id="93485-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="93485-105">Een Redis-Cache maken met behulp van IntelliJ</span><span class="sxs-lookup"><span data-stu-id="93485-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="93485-106">Hallo stappen doorlopen Hallo stappen toocreate een redis-cache met behulp van hello Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="93485-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="93485-107">Meld u aan tooyour Azure-account met Hallo stappen in Hallo [aanmelding In instructies voor het hello Azure Toolkit voor IntelliJ] artikel.</span><span class="sxs-lookup"><span data-stu-id="93485-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="93485-108">In Hallo **Azure Explorer** venster hulpprogramma uit, vouw Hallo **Azure** knooppunt met de rechtermuisknop op **Redis-Caches**, en klik vervolgens op **Redis-Cache maken**.</span><span class="sxs-lookup"><span data-stu-id="93485-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Menu Redis-Cache maken][CR01]

1. <span data-ttu-id="93485-110">Wanneer Hallo **nieuwe Redis-Cache** dialoogvenster wordt weergegeven, Hallo volgende opties opgeven:</span><span class="sxs-lookup"><span data-stu-id="93485-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Dialoogvenster Nieuwe Redis-Cache maken][CR02]

   <span data-ttu-id="93485-112">a.</span><span class="sxs-lookup"><span data-stu-id="93485-112">a.</span></span> <span data-ttu-id="93485-113">**DNS-naam**: Hiermee geeft u de DNS-subdomein Hallo voor Hallo nieuwe redis-cache, die worden voorafgegaan te '. redis.cache.windows .net "; bijvoorbeeld: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="93485-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="93485-114">b.</span><span class="sxs-lookup"><span data-stu-id="93485-114">b.</span></span> <span data-ttu-id="93485-115">**Abonnement**: Hiermee geeft u hello Azure-abonnement u toouse voor de nieuwe redis-cache hello wilt.</span><span class="sxs-lookup"><span data-stu-id="93485-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="93485-116">c.</span><span class="sxs-lookup"><span data-stu-id="93485-116">c.</span></span> <span data-ttu-id="93485-117">**Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor redis-cache; moet u toochoose Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="93485-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="93485-118">**Maken van nieuw**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="93485-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="93485-119">**Gebruik bestaande**: Hiermee geeft u op dat u uit een lijst met resourcegroepen die zijn gekoppeld aan uw Azure-account kiest.</span><span class="sxs-lookup"><span data-stu-id="93485-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="93485-120">d.</span><span class="sxs-lookup"><span data-stu-id="93485-120">d.</span></span> <span data-ttu-id="93485-121">**Locatie**: Hiermee geeft u Hallo-locatie waar uw redis-cache wordt gemaakt; bijvoorbeeld *VS-West*.</span><span class="sxs-lookup"><span data-stu-id="93485-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="93485-122">e.</span><span class="sxs-lookup"><span data-stu-id="93485-122">e.</span></span> <span data-ttu-id="93485-123">**Prijscategorie**: Hiermee geeft u op welke prijscategorie uw redis-cache wordt gebruikt; deze instelling bepaalt u het aantal clientverbindingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="93485-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="93485-124">(Zie voor meer informatie [Redis-Cache prijzen].)</span><span class="sxs-lookup"><span data-stu-id="93485-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="93485-125">f.</span><span class="sxs-lookup"><span data-stu-id="93485-125">f.</span></span> <span data-ttu-id="93485-126">**Niet-SSL-poort**: Hiermee geeft u op of de redis-cache niet-SSL-verbindingen toestaat; standaard SSL-verbindingen zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="93485-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="93485-127">Wanneer u alle instellingen van uw redis-cache hebt opgegeven, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="93485-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="93485-128">Nadat uw redis-cache is gemaakt, wordt deze in hello Azure Explorer worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="93485-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Redis-Cache in Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="93485-130">Voor meer informatie over het configureren van uw Azure redis-cache-instellingen, Zie [hoe tooconfigure Azure Redis-Cache].</span><span class="sxs-lookup"><span data-stu-id="93485-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="93485-131">Hallo-eigenschappen voor uw Redis-Cache in IntelliJ weergeven</span><span class="sxs-lookup"><span data-stu-id="93485-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="93485-132">In Azure Explorer hello, met de rechtermuisknop op uw redis-cache en klik op **eigenschappen weergeven**.</span><span class="sxs-lookup"><span data-stu-id="93485-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer toodisplay eigenschappen van contextmenu voor een redis-cache][SP01]

1. <span data-ttu-id="93485-134">Hello Azure Explorer weergeven Hallo-eigenschappen voor uw redis-cache</span><span class="sxs-lookup"><span data-stu-id="93485-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Eigenschappen van Redis-cache][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="93485-136">Verwijderen van uw Redis-Cache met behulp van IntelliJ</span><span class="sxs-lookup"><span data-stu-id="93485-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="93485-137">In Azure Explorer hello, met de rechtermuisknop op uw redis-cache en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="93485-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure Explorer context menu toodelete een redis-cache][DE01]

1. <span data-ttu-id="93485-139">Klik op **Ja** wanneer u daarom wordt gevraagd toodelete redis-cache.</span><span class="sxs-lookup"><span data-stu-id="93485-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![Prompt voor redis-cache verwijderen][DE02]

## <a name="next-steps"></a><span data-ttu-id="93485-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93485-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="93485-142">Zie voor meer informatie over Azure redis-caches, configuratie-instellingen en prijzen Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="93485-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="93485-143">[Azure Redis-cache]</span><span class="sxs-lookup"><span data-stu-id="93485-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="93485-144">[Redis-Cache-documentatie]</span><span class="sxs-lookup"><span data-stu-id="93485-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="93485-145">[Redis-Cache prijzen]</span><span class="sxs-lookup"><span data-stu-id="93485-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="93485-146">[hoe tooconfigure Azure Redis-Cache]</span><span class="sxs-lookup"><span data-stu-id="93485-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Redis-Cache prijzen]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis-cache]: https://azure.microsoft.com/services/cache/
[Redis-Cache-documentatie]: ./redis-cache/index.md
[hoe tooconfigure Azure Redis-Cache]: ./redis-cache/cache-configure.md
[aanmelding In instructies voor het hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
