---
title: Het beheren van Redis-cache met behulp van de Azure-Explorer voor IntelliJ | Microsoft Docs
description: Informatie over het beheren van uw Azure redis-caches met behulp van de Azure-Explorer voor IntelliJ.
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
ms.openlocfilehash: 9ab8ae17ee2a92b5b16d2210366c00b5b8023fa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="a0765-103">Met de Azure-Explorer voor IntelliJ Redis-Caches beheren</span><span class="sxs-lookup"><span data-stu-id="a0765-103">Managing Redis Caches using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="a0765-104">De Azure-Explorer, die deel van de Azure-werkset voor IntelliJ uitmaakt, biedt de redis-caches in de Azure-account uit binnen de IntelliJ IDE voor Java-ontwikkelaars met een eenvoudig-en-klare oplossing voor het beheren van.</span><span class="sxs-lookup"><span data-stu-id="a0765-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="a0765-105">Een Redis-Cache maken met behulp van IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a0765-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="a0765-106">De volgende stappen maakt u de stappen voor het maken van een redis-cache met behulp van de Azure-Explorer.</span><span class="sxs-lookup"><span data-stu-id="a0765-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="a0765-107">Aanmelden bij uw Azure-account met behulp van de stappen in de [aanmelding In instructies voor de Azure-werkset voor IntelliJ] artikel.</span><span class="sxs-lookup"><span data-stu-id="a0765-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="a0765-108">In de **Azure Explorer** venster hulpprogramma uit, vouw de **Azure** knooppunt met de rechtermuisknop op **Redis-Caches**, en klik vervolgens op **Redis-Cache maken**.</span><span class="sxs-lookup"><span data-stu-id="a0765-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Menu Redis-Cache maken][CR01]

1. <span data-ttu-id="a0765-110">Wanneer de **nieuwe Redis-Cache** dialoogvenster wordt weergegeven, geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="a0765-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Dialoogvenster Nieuwe Redis-Cache maken][CR02]

   <span data-ttu-id="a0765-112">a.</span><span class="sxs-lookup"><span data-stu-id="a0765-112">a.</span></span> <span data-ttu-id="a0765-113">**DNS-naam**: Hiermee geeft u het DNS-subdomein voor de nieuwe redis-cache, die functienaam worden geplaatst om '. redis.cache.windows.net "; bijvoorbeeld: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="a0765-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which are prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="a0765-114">b.</span><span class="sxs-lookup"><span data-stu-id="a0765-114">b.</span></span> <span data-ttu-id="a0765-115">**Abonnement**: Hiermee geeft u het Azure-abonnement u wilt gebruiken voor de nieuwe redis-cache.</span><span class="sxs-lookup"><span data-stu-id="a0765-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="a0765-116">c.</span><span class="sxs-lookup"><span data-stu-id="a0765-116">c.</span></span> <span data-ttu-id="a0765-117">**Resourcegroep**: Hiermee geeft u de resourcegroep voor uw redis-cache; u moet een van de volgende opties kiezen:</span><span class="sxs-lookup"><span data-stu-id="a0765-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="a0765-118">**Maken van nieuw**: geeft aan dat u wilt maken van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a0765-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="a0765-119">**Gebruik bestaande**: Hiermee geeft u op dat u uit een lijst met resourcegroepen die zijn gekoppeld aan uw Azure-account kiest.</span><span class="sxs-lookup"><span data-stu-id="a0765-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="a0765-120">d.</span><span class="sxs-lookup"><span data-stu-id="a0765-120">d.</span></span> <span data-ttu-id="a0765-121">**Locatie**: Hiermee geeft u de locatie waar uw redis-cache wordt gemaakt; bijvoorbeeld *VS-West*.</span><span class="sxs-lookup"><span data-stu-id="a0765-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="a0765-122">e.</span><span class="sxs-lookup"><span data-stu-id="a0765-122">e.</span></span> <span data-ttu-id="a0765-123">**Prijscategorie**: Hiermee geeft u op welke prijscategorie uw redis-cache wordt gebruikt; deze instelling bepaalt u het aantal verbindingen van clients.</span><span class="sxs-lookup"><span data-stu-id="a0765-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="a0765-124">(Zie voor meer informatie [Redis-Cache prijzen].)</span><span class="sxs-lookup"><span data-stu-id="a0765-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="a0765-125">f.</span><span class="sxs-lookup"><span data-stu-id="a0765-125">f.</span></span> <span data-ttu-id="a0765-126">**Niet-SSL-poort**: Hiermee geeft u op of de redis-cache niet-SSL-verbindingen toestaat; standaard SSL-verbindingen zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="a0765-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="a0765-127">Wanneer u alle instellingen van uw redis-cache hebt opgegeven, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0765-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="a0765-128">Nadat uw redis-cache is gemaakt, wordt deze weergegeven in de Azure-Explorer.</span><span class="sxs-lookup"><span data-stu-id="a0765-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Redis-Cache in Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="a0765-130">Voor meer informatie over het configureren van uw Azure redis-cache-instellingen, Zie [het configureren van Azure Redis-Cache].</span><span class="sxs-lookup"><span data-stu-id="a0765-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="a0765-131">De eigenschappen voor uw Redis-Cache in IntelliJ weergeven</span><span class="sxs-lookup"><span data-stu-id="a0765-131">Display the properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="a0765-132">In de Azure-Explorer met de rechtermuisknop op uw redis-cache en klikt u op **eigenschappen weergeven**.</span><span class="sxs-lookup"><span data-stu-id="a0765-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer contextmenu Eigenschappen weergeven voor een redis-cache][SP01]

1. <span data-ttu-id="a0765-134">De Azure-Explorer geeft de eigenschappen voor uw redis-cache.</span><span class="sxs-lookup"><span data-stu-id="a0765-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Eigenschappen van Redis-cache][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="a0765-136">Verwijderen van uw Redis-Cache met behulp van IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a0765-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="a0765-137">In de Azure-Explorer met de rechtermuisknop op uw redis-cache en klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="a0765-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure Explorer contextmenu een redis-cache verwijderen][DE01]

1. <span data-ttu-id="a0765-139">Klik op **Ja** wanneer u wordt gevraagd uw redis-cache verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a0765-139">Click **Yes** when prompted to delete your redis cache.</span></span>

   ![Prompt voor redis-cache verwijderen][DE02]

## <a name="next-steps"></a><span data-ttu-id="a0765-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0765-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="a0765-142">Zie de volgende koppelingen voor meer informatie over Azure redis-caches, configuratie-instellingen en prijzen:</span><span class="sxs-lookup"><span data-stu-id="a0765-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="a0765-143">[Azure Redis-cache]</span><span class="sxs-lookup"><span data-stu-id="a0765-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="a0765-144">[Redis-Cache-documentatie]</span><span class="sxs-lookup"><span data-stu-id="a0765-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="a0765-145">[Redis-Cache prijzen]</span><span class="sxs-lookup"><span data-stu-id="a0765-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="a0765-146">[het configureren van Azure Redis-Cache]</span><span class="sxs-lookup"><span data-stu-id="a0765-146">[How to configure Azure Redis Cache]</span></span>

<!-- URL List -->

<span data-ttu-id="a0765-147">[Redis-Cache prijzen]: https://azure.microsoft.com/pricing/details/cache/</span><span class="sxs-lookup"><span data-stu-id="a0765-147">[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/</span></span>
<span data-ttu-id="a0765-148">[Azure Redis-cache]: https://azure.microsoft.com/services/cache/</span><span class="sxs-lookup"><span data-stu-id="a0765-148">[Azure Redis Cache]: https://azure.microsoft.com/services/cache/</span></span>
<span data-ttu-id="a0765-149">[Redis-Cache-documentatie]: ./redis-cache/index.md</span><span class="sxs-lookup"><span data-stu-id="a0765-149">[Redis Cache Documentation]: ./redis-cache/index.md</span></span>
<span data-ttu-id="a0765-150">[het configureren van Azure Redis-Cache]: ./redis-cache/cache-configure.md</span><span class="sxs-lookup"><span data-stu-id="a0765-150">[How to configure Azure Redis Cache]: ./redis-cache/cache-configure.md</span></span>
<span data-ttu-id="a0765-151">[aanmelding In instructies voor de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="a0765-151">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
