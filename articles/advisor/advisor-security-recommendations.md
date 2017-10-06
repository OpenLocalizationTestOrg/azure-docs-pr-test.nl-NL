---
title: Aanbevelingen voor beveiliging van Advisor aaaAzure | Microsoft Docs
description: Gebruik Azure Advisor toohelp Hallo beveiliging van uw Azure-implementaties te verbeteren.
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
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="20814-103">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="20814-103">Advisor Security recommendations</span></span>

<span data-ttu-id="20814-104">Azure Advisor biedt een consistente, geconsolideerde weergave van aanbevelingen voor alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="20814-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="20814-105">Het is geïntegreerd met Azure Security Center toobring u aanbevelingen voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="20814-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="20814-106">U krijgt aanbevelingen voor beveiliging van Hallo **beveiliging** tabblad op Hallo Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="20814-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![Hallo-knop van Advisor-beveiliging](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="20814-108">Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="20814-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="20814-109">Periodiek wordt geanalyseerd Hallo beveiligingsstatus van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="20814-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="20814-110">Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="20814-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="20814-111">Hallo aanbevelingen helpen u bij Hallo configuratieproces Hallo besturingselementen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="20814-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![tabblad van de Advisor-beveiliging Hallo](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="20814-113">Zie voor meer informatie over beveiligingsaanbevelingen [aanbevelingen voor beveiliging in Azure Security Center beheren](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="20814-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="20814-114">Hoe tooaccess aanbevelingen voor beveiliging in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="20814-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="20814-115">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20814-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="20814-116">Klik in het linkerdeelvenster Hallo **meer services**.</span><span class="sxs-lookup"><span data-stu-id="20814-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="20814-117">Service in Hallo menu deelvenster onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="20814-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="20814-118">Hallo Advisor dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="20814-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="20814-119">Klik op Hallo Advisor dashboard Hallo **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="20814-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="20814-120">Selecteer Hallo abonnement waarvoor u wilt dat tooreceive aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="20814-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="20814-121">tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="20814-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="20814-122">Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="20814-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="20814-123">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="20814-123">This is a *one-time operation*.</span></span> <span data-ttu-id="20814-124">Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.</span><span class="sxs-lookup"><span data-stu-id="20814-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20814-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20814-125">Next steps</span></span>

<span data-ttu-id="20814-126">toolearn meer informatie over de aanbevelingen van Advisor, Zie:</span><span class="sxs-lookup"><span data-stu-id="20814-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="20814-127">Inleiding tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="20814-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="20814-128">Aan de slag met Advisor</span><span class="sxs-lookup"><span data-stu-id="20814-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="20814-129">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="20814-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="20814-130">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="20814-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="20814-131">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="20814-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
