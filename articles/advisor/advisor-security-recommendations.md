---
title: Beveiligingsaanbevelingen voor de Azure Advisor | Microsoft Docs
description: Gebruik Azure Advisor om te helpen verbeteren de beveiliging van uw Azure-implementaties.
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="9617f-103">Aanbevelingen voor beveiliging van Advisor</span><span class="sxs-lookup"><span data-stu-id="9617f-103">Advisor Security recommendations</span></span>

<span data-ttu-id="9617f-104">Azure Advisor biedt een consistente, geconsolideerde weergave van aanbevelingen voor alle Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9617f-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="9617f-105">Het is geïntegreerd met Azure Security Center zodat u aanbevelingen voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9617f-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="9617f-106">U krijgt aanbevelingen voor beveiliging van de **beveiliging** op het dashboard Advisor.</span><span class="sxs-lookup"><span data-stu-id="9617f-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![De knop Advisor-beveiliging](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="9617f-108">Azure Security Center helpt u bij het detecteren, voorkomen van en reageren op bedreigingen dankzij een verhoogde zichtbaarheid van en controle over de beveiliging van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9617f-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="9617f-109">Er worden regelmatig de beveiligingsstatus van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9617f-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="9617f-110">Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="9617f-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="9617f-111">De aanbevelingen leiden u door het configuratieproces van de besturingselementen die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="9617f-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Het tabblad Beveiliging van Advisor](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="9617f-113">Zie voor meer informatie over beveiligingsaanbevelingen [aanbevelingen voor beveiliging in Azure Security Center beheren](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="9617f-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="9617f-114">Toegang tot de aanbevelingen voor beveiliging in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="9617f-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="9617f-115">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9617f-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9617f-116">Klik in het linkerdeelvenster op **meer services**.</span><span class="sxs-lookup"><span data-stu-id="9617f-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="9617f-117">Klik in het deelvenster service menu onder **bewaking en beheer**, klikt u op **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="9617f-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="9617f-118">De Advisor-dashboard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9617f-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="9617f-119">Klik op het dashboard Advisor de **beveiliging** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9617f-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="9617f-120">Selecteer het abonnement waarvoor u wilt ontvangen van aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.</span><span class="sxs-lookup"><span data-stu-id="9617f-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="9617f-121">Voor toegang tot de aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor.</span><span class="sxs-lookup"><span data-stu-id="9617f-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="9617f-122">Een abonnement is geregistreerd als een *abonnement eigenaar* start van de Advisor-dashboard en klikt op de **aanbevelingen krijgen** knop.</span><span class="sxs-lookup"><span data-stu-id="9617f-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="9617f-123">Dit is een *eenmalige bewerking*.</span><span class="sxs-lookup"><span data-stu-id="9617f-123">This is a *one-time operation*.</span></span> <span data-ttu-id="9617f-124">Nadat het abonnement is geregistreerd, kunt u de aanbevelingen van Advisor als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, resourcegroep of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="9617f-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9617f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9617f-125">Next steps</span></span>

<span data-ttu-id="9617f-126">Zie voor meer informatie over Advisor aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="9617f-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="9617f-127">Inleiding tot Advisor</span><span class="sxs-lookup"><span data-stu-id="9617f-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="9617f-128">Aan de slag met Advisor</span><span class="sxs-lookup"><span data-stu-id="9617f-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="9617f-129">Advisor kosten aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="9617f-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="9617f-130">Aanbevelingen van Advisor-prestaties</span><span class="sxs-lookup"><span data-stu-id="9617f-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="9617f-131">Hoge beschikbaarheid aanbevelingen Advisor te ontvangen</span><span class="sxs-lookup"><span data-stu-id="9617f-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
