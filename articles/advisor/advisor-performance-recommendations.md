---
title: Azure Advisor prestaties aanbevelingen | Microsoft Docs
description: Advisor gebruiken om de prestaties van uw Azure-implementaties te optimaliseren.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="fffab-103">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="fffab-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="fffab-104">Azure aanbevelingen van Advisor prestaties te verbeteren en de reactiesnelheid van uw bedrijfskritieke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fffab-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="fffab-105">U kunt prestaties aanbevelingen van Advisor ophalen op de **prestaties** van de Advisor-dashboard.</span><span class="sxs-lookup"><span data-stu-id="fffab-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Tabblad van Advisor-prestaties](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="fffab-107">Verbeteren de databaseprestaties met SQL database Advisor</span><span class="sxs-lookup"><span data-stu-id="fffab-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="fffab-108">Advisor biedt een consistente, geconsolideerde weergave van aanbevelingen voor alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="fffab-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="fffab-109">Het is geïntegreerd met SQL Database Advisor zodat u de aanbevelingen voor het verbeteren van de prestaties van uw Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="fffab-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="fffab-110">SQL Database Advisor beoordeelt de prestaties van uw Azure SQL-database door een analyse van uw gebruiksgeschiedenis.</span><span class="sxs-lookup"><span data-stu-id="fffab-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="fffab-111">Deze biedt aanbevelingen die geschikt zijn voor het uitvoeren van de normale werkbelasting van de database vervolgens.</span><span class="sxs-lookup"><span data-stu-id="fffab-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="fffab-112">Als u de aanbevelingen, moet een database over een week van het gebruik van, en binnen een week moet er een consistente activiteit.</span><span class="sxs-lookup"><span data-stu-id="fffab-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="fffab-113">SQL Database Advisor kunt eenvoudiger voor consistente querypatronen dan voor willekeurige lichtflitsen activiteit optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="fffab-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="fffab-114">Zie voor meer informatie over SQL Database Advisor [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="fffab-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Aanbevelingen voor SQL-database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="fffab-116">De Redis-Cache-prestaties en betrouwbaarheid verbeteren</span><span class="sxs-lookup"><span data-stu-id="fffab-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="fffab-117">Advisor identificeert exemplaren van Redis-Cache waarbij prestaties mogelijk negatief beïnvloed door hoog geheugengebruik, serverbelasting, bandbreedte van het netwerk of een groot aantal clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="fffab-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="fffab-118">Advisor biedt ook aanbevolen procedures aanbevelingen om te voorkomen, potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="fffab-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="fffab-119">Zie voor meer informatie over Redis-Cache aanbevelingen [Redis-Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="fffab-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="fffab-120">App Service-prestaties en betrouwbaarheid te verbeteren</span><span class="sxs-lookup"><span data-stu-id="fffab-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="fffab-121">Azure Advisor kan worden geïntegreerd met aanbevelingen voor uw App Services-ervaring te verbeteren en relevante platformmogelijkheden detecteren.</span><span class="sxs-lookup"><span data-stu-id="fffab-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="fffab-122">Voorbeelden van App Services aanbevelingen zijn:</span><span class="sxs-lookup"><span data-stu-id="fffab-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="fffab-123">Detectie van exemplaren waar het geheugen of CPU-bronnen zijn uitgeput door app runtimes met risicobeperking opties.</span><span class="sxs-lookup"><span data-stu-id="fffab-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="fffab-124">Detectie van exemplaren waar collocating resources, zoals web-apps en -databases kan de prestaties en lagere kosten verbeteren.</span><span class="sxs-lookup"><span data-stu-id="fffab-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="fffab-125">Zie voor meer informatie over App-Services aanbevelingen [aanbevolen procedures voor het Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="fffab-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="fffab-126">![Aanbevelingen voor App-Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="fffab-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="fffab-127">Toegang tot de aanbevelingen van de prestaties in Advisor</span><span class="sxs-lookup"><span data-stu-id="fffab-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="fffab-128">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fffab-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fffab-129">Klik in het linkerdeelvenster op **meer services**.</span><span class="sxs-lookup"><span data-stu-id="fffab-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="fffab-130">Klik in het deelvenster service menu onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="fffab-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="fffab-131">De Advisor-dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fffab-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="fffab-132">Klik op het dashboard Advisor de **prestaties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fffab-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="fffab-133">Selecteer het abonnement waarvoor u wilt ontvangen van aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="fffab-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="fffab-134">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="fffab-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="fffab-135">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="fffab-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="fffab-136">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="fffab-136">This is a *one-time operation*.</span></span> <span data-ttu-id="fffab-137">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="fffab-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fffab-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fffab-138">Next steps</span></span>

<span data-ttu-id="fffab-139">Zie voor meer informatie over Advisor aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="fffab-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="fffab-140">Inleiding tot Advisor</span><span class="sxs-lookup"><span data-stu-id="fffab-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="fffab-141">Aan de slag met Advisor</span><span class="sxs-lookup"><span data-stu-id="fffab-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="fffab-142">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="fffab-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="fffab-143">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="fffab-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="fffab-144">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="fffab-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

