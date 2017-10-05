---
title: Aan de slag met Azure Advisor | Microsoft Docs
description: Aan de slag met Azure Advisor.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="8d262-103">Aan de slag met Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="8d262-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="8d262-104">Informatie over het Advisor toegang via de Azure portal, aanbevelingen krijgen, implementeer aanbevelingen, zoeken naar aanbevelingen en aanbevelingen voor vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="8d262-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="8d262-105">Ontvang aanbevelingen van Advisor</span><span class="sxs-lookup"><span data-stu-id="8d262-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="8d262-106">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d262-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8d262-107">Klik in het linkerdeelvenster op **meer services**.</span><span class="sxs-lookup"><span data-stu-id="8d262-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="8d262-108">Klik in het deelvenster service menu onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="8d262-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="8d262-109">De Advisor-dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8d262-109">The Advisor dashboard is displayed.</span></span>

   ![Toegang tot Azure Advisor met de Azure portal](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="8d262-111">Selecteer het abonnement waarvoor u wilt ontvangen van aanbevelingen op het dashboard Advisor.</span><span class="sxs-lookup"><span data-stu-id="8d262-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="8d262-112">De Advisor-dashboard toont de persoonlijke aanbevelingen voor een geselecteerde abonnement.</span><span class="sxs-lookup"><span data-stu-id="8d262-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="8d262-113">Als u de aanbevelingen voor een bepaalde categorie, klikt u op een van de tabbladen: **hoge beschikbaarheid**, **beveiliging**, **prestaties**, of **kosten**.</span><span class="sxs-lookup"><span data-stu-id="8d262-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="8d262-114">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="8d262-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="8d262-115">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="8d262-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="8d262-116">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="8d262-116">This is a *one-time operation*.</span></span> <span data-ttu-id="8d262-117">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="8d262-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Advisor-dashboard](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="8d262-119">Details van de Advisor-aanbeveling ophalen en implementeren van een oplossing</span><span class="sxs-lookup"><span data-stu-id="8d262-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="8d262-120">De **aanbeveling** blade in Advisor biedt aanvullende informatie over de aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="8d262-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="8d262-121">Aanmelden bij de [Azure-portal](https://portal.azure.com), en start vervolgens [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="8d262-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="8d262-122">Op de **Advisor aanbevelingen** dashboard, klikt u op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="8d262-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="8d262-123">Klik in de lijst met aanbevelingen op een aanbeveling die u wilt controleren in detail.</span><span class="sxs-lookup"><span data-stu-id="8d262-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="8d262-124">De **aanbeveling** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8d262-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="8d262-125">Op de **aanbevelingen** blade gegevens bekijken over acties die u kunt uitvoeren als een mogelijk probleem wilt oplossen of profiteren van een kans kosten te besparen.</span><span class="sxs-lookup"><span data-stu-id="8d262-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![De Advisor-indexaanbeveling](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="8d262-127">Zoeken naar Advisor aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="8d262-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="8d262-128">U kunt zoeken naar aanbevelingen voor een bepaalde groep abonnement of resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8d262-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="8d262-129">U kunt ook zoeken aanbevelingen op status.</span><span class="sxs-lookup"><span data-stu-id="8d262-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="8d262-130">Aanmelden bij de [Azure-portal](https://portal.azure.com), en start vervolgens [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="8d262-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="8d262-131">Zoeken naar aanbevelingen op filteren voor abonnementen en resourcegroepen aanbeveling status (**Active** of **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="8d262-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="8d262-132">Een lijst met aanbevelingen Advisor te ontvangen die zijn gebaseerd op uw zoekopdracht filtercriteria, klikt u op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="8d262-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Advisor zoekfilter criteria](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="8d262-134">Uitstellen of negeren van Advisor aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="8d262-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="8d262-135">Aanmelden bij de [Azure-portal](https://portal.azure.com), en start vervolgens [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="8d262-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="8d262-136">Klik op **aanbevelingen krijgen**, en klik vervolgens in de lijst met aanbevelingen op een aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="8d262-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="8d262-137">Op de **aanbeveling** blade, klikt u op **uitstellen**.</span><span class="sxs-lookup"><span data-stu-id="8d262-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Voorbeeld van Advisor aanbeveling actie](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="8d262-139">Geef een periode bewerkingen worden uitgesteld of selecteer **nooit** naar de aanbeveling negeren.</span><span class="sxs-lookup"><span data-stu-id="8d262-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8d262-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d262-140">Next steps</span></span>

<span data-ttu-id="8d262-141">Zie voor meer informatie over Advisor:</span><span class="sxs-lookup"><span data-stu-id="8d262-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="8d262-142">Inleiding tot Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="8d262-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="8d262-143">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="8d262-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="8d262-144">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="8d262-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="8d262-145">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="8d262-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="8d262-146">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="8d262-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
