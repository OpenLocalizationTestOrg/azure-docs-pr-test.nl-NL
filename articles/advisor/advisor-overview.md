---
title: Inleiding tot Azure Advisor | Microsoft Docs
description: Gebruik Azure Advisor om te optimaliseren van uw Azure-implementaties.
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
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="b6e9c-103">Inleiding tot Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="b6e9c-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="b6e9c-104">Meer informatie over Azure Advisor en de belangrijkste mogelijkheden en antwoorden op veelgestelde vragen.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="b6e9c-105">Wat is Advisor?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-105">What is Advisor?</span></span>
<span data-ttu-id="b6e9c-106">Advisor is een persoonlijke cloud-consultant waarmee u Volg de aanbevolen procedures om uw Azure-implementaties te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="b6e9c-107">Het analyseert uw resourceconfiguratie en de telemetrie van de informatie over het gebruik en vervolgens raadt aan om de oplossingen waarmee u de kosteneffectiviteit, prestaties, beschikbaarheid en beveiliging van uw Azure-resources te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="b6e9c-108">Met Advisor, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b6e9c-108">With Advisor, you can:</span></span>
* <span data-ttu-id="b6e9c-109">Proactieve, bruikbare ophalen en gepersonaliseerde aanbevolen procedures.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="b6e9c-110">Verbeteren de prestaties, beveiliging en hoge beschikbaarheid van uw resources, zoals u Identificeer mogelijkheden om te beperken van uw algehele Azure hoeven te besteden aan.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="b6e9c-111">Aanbevelingen met voorgestelde acties inline worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="b6e9c-112">U hebt toegang tot Advisor via de [Azure-portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="b6e9c-113">Aanmelden bij de [portal](https://portal.azure.com), selecteer **Bladeren**, en schuif vervolgens naar **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="b6e9c-114">De Advisor-dashboard toont de persoonlijke aanbevelingen voor een geselecteerde abonnement.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="b6e9c-115">De aanbevelingen worden onderverdeeld in vier categorieën:</span><span class="sxs-lookup"><span data-stu-id="b6e9c-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="b6e9c-116">**Hoge beschikbaarheid**: om te controleren en de continuïteit van uw bedrijfskritieke toepassingen te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="b6e9c-117">Zie voor meer informatie [aanbevelingen voor hoge beschikbaarheid van Advisor](advisor-high-availability-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="b6e9c-118">**Beveiliging**: voor het detecteren van bedreigingen en zwakke plekken die tot beveiligingsrisico's leiden mogelijk.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="b6e9c-119">Zie voor meer informatie [Advisor beveiligingsaanbevelingen](advisor-security-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="b6e9c-120">**Prestaties**: voor het verbeteren van de snelheid van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="b6e9c-121">Zie voor meer informatie [Advisor prestaties aanbevelingen](advisor-performance-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="b6e9c-122">**Kosten**: te optimaliseren en reduceren uw algehele Azure besteden.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="b6e9c-123">Zie voor meer informatie [aanbevelingen van Advisor kosten](advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Advisor aanbeveling typen](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="b6e9c-125">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="b6e9c-126">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="b6e9c-127">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-127">This is a *one-time operation*.</span></span> <span data-ttu-id="b6e9c-128">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="b6e9c-129">U kunt klikken op een aanbeveling voor meer informatie over deze.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="b6e9c-130">U kunt ook meer informatie over acties die u uitvoeren kunt om te profiteren van een kans of een probleem oplost.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="b6e9c-131">Advisor biedt aanbevelingen met inline acties of documentatie koppelingen.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="b6e9c-132">Te klikken op een inline-actie doorloopt u via een 'begeleide gebruiker reis' om dit te implementeren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="b6e9c-133">Een documentatie-koppeling te klikken, wordt u verwijst naar documentatie die wordt beschreven hoe u de actie handmatig implementeren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="b6e9c-134">Advisor updates aanbevelingen per uur.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="b6e9c-135">Als u niet dat onmiddellijk actie ondernemen op een aanbeveling wilt, kunt u deze uitstellen voor een opgegeven periode of genegeerd.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="b6e9c-136">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="b6e9c-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="b6e9c-137">Hoe krijg ik toegang tot Advisor?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-137">How do I access Advisor?</span></span>
<span data-ttu-id="b6e9c-138">U hebt toegang tot Advisor via de [Azure-portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="b6e9c-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="b6e9c-139">Aanmelden bij de [portal](https://portal.azure.com), selecteer **Bladeren**, en schuif vervolgens naar **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="b6e9c-140">De Advisor-dashboard toont de persoonlijke aanbevelingen voor een geselecteerde abonnement.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="b6e9c-141">U kunt ook aanbevelingen van Advisor weergeven via de resourceblade van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="b6e9c-142">Kies een virtuele machine en schuif vervolgens naar de Advisor-aanbevelingen in het menu.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="b6e9c-143">Welke machtigingen heb ik nodig voor toegang tot Advisor?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="b6e9c-144">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="b6e9c-145">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="b6e9c-146">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-146">This is a *one-time operation*.</span></span> <span data-ttu-id="b6e9c-147">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="b6e9c-148">Hoe vaak worden aanbevelingen van Advisor bijgewerkt?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="b6e9c-149">Advisor aanbevelingen worden elk uur bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="b6e9c-150">Welke bronnen biedt Advisor aanbevelingen voor?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="b6e9c-151">Advisor bevat aanbevelingen voor virtuele machines, beschikbaarheidssets Toepassingsgateways, App-Services, SQL-servers, SQL-databases en Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="b6e9c-152">Kan ik uitstellen of een aanbeveling negeren?</span><span class="sxs-lookup"><span data-stu-id="b6e9c-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="b6e9c-153">Als u wilt uitstellen of een aanbeveling negeren, klikt u op de **uitstellen** knop of koppeling.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="b6e9c-154">U kunt opgeven dat een tijd uitstellen periode of selecteer **nooit** naar de aanbeveling negeren.</span><span class="sxs-lookup"><span data-stu-id="b6e9c-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6e9c-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6e9c-155">Next steps</span></span>

<span data-ttu-id="b6e9c-156">Zie voor meer informatie over Advisor aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="b6e9c-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="b6e9c-157">Aan de slag met Advisor</span><span class="sxs-lookup"><span data-stu-id="b6e9c-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="b6e9c-158">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="b6e9c-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="b6e9c-159">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="b6e9c-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="b6e9c-160">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="b6e9c-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="b6e9c-161">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="b6e9c-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
