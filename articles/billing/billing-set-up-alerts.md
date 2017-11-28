---
title: aaaSet van facturerings- of waarschuwingen voor Azure-abonnementen | Microsoft Docs
description: Hierin wordt beschreven hoe u kunt waarschuwingen instellen op uw Azure-factuur zodat u kunt facturering verrassingen vermijden.
keywords: tegoed waarschuwing facturering waarschuwing
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="fe6eb-104">Facturerings- of waarschuwingen instellen voor uw Microsoft Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="fe6eb-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="fe6eb-105">Als u Hallo beheerder van het Account voor een Azure-abonnement bent, kunt u hello Azure Billing waarschuwingsservice toocreate aangepast facturering waarschuwingen die helpen u te bewaken en beheren van activiteit facturering voor uw Azure-accounts.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="fe6eb-106">Deze service is in de preview, dus u tooenable het Hallo Voorbeeldfuncties pagina eerst moet.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="fe6eb-107">Hallo drempelwaarde en e-mail ontvangers instellen</span><span class="sxs-lookup"><span data-stu-id="fe6eb-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="fe6eb-108">Ga naar [Hallo Voorbeeldfuncties pagina](https://account.windowsazure.com/PreviewFeatures) en schakel **waarschuwingsservice facturering**.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="fe6eb-109">Nadat u Hallo e-mailbevestiging die facturering Hallo-service is ingeschakeld voor uw abonnement ontvangt, gaat u naar [Hallo abonnementen pagina](https://account.windowsazure.com/Subscriptions) in Hallo-accountportal.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="fe6eb-110">Klik op Hallo abonnement u wilt toomonitor en klik vervolgens op **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Schermafbeelding van de weergave van de abonnementen Hallo van Azure-accountcentrum, met waarschuwingen die zijn gemarkeerd][Image1]

2. <span data-ttu-id="fe6eb-112">Klik vervolgens op **waarschuwing toevoegen** toocreate zelf een.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="fe6eb-113">U kunt een totaal van vijf factureringsmeldingen per abonnement, met een andere drempelwaarde en omhoog in de e-mailontvangers tootwo voor elke waarschuwing instellen.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Schermopname van Hallo waarschuwingen weergeven, waarin u de waarschuwing kunt toevoegen][Image2]

3. <span data-ttu-id="fe6eb-115">Wanneer u een waarschuwing toevoegt, u een unieke naam geven, kies een bestedingslimiet drempelwaarde en kies Hallo e-mailadressen waarop waarschuwingen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="fe6eb-116">Bij het instellen van Hallo drempelwaarde, kunt u ofwel een **totale facturering** of een **financieel tegoed** van Hallo **waarschuwing voor** lijst.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="fe6eb-117">Voor een totaal facturering, wordt een waarschuwing verzonden wanneer Hallo abonnement uitgaven overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="fe6eb-118">Voor een financieel tegoed is een waarschuwing verzonden wanneer monetaire krediet Hallo limiet beneden.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="fe6eb-119">Monetaire krediet doorgaans tooFree proefversie en Visual Studio-abonnementen van toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Schermopname van Hallo waarschuwing toevoeging weergave, waar u de geadresseerden kunt configureren][Image3]

<span data-ttu-id="fe6eb-121">Azure biedt ondersteuning voor elk e-mailadres, maar niet controleren of de e-mailadres Hallo werkt, dus Controleer op typefouten.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="fe6eb-122">Controleer op waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="fe6eb-122">Check on your alerts</span></span>
<span data-ttu-id="fe6eb-123">Na het instellen van waarschuwingen, bevat deze hello Accountcentrum- en ziet u hoe veel meer kunt u instellen.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="fe6eb-124">Voor elke waarschuwing ziet u Hallo datum en tijdstip van verzending, of het om een waarschuwing voor totale facturering of financieel tegoed en Hallo limiet die u instelt.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="fe6eb-125">Hallo datum- en tijdnotatie is coördineren 24-uurs-Universal Time (UTC) en Hallo datum is jjjj-mm-dd-indeling.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="fe6eb-126">Klik op Hallo plus ondertekenen voor een waarschuwing in Hallo lijst tooedit of Hallo-Prullenbak toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="fe6eb-127">Waarschuwingen voor facturering voor klanten met Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="fe6eb-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="fe6eb-128">EA klanten kunnen waarschuwingen krijgen voor elke afdeling onder een inschrijving door de instelling uitgaven quota's.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="fe6eb-129">Zie [afdeling uitgaven quota](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in Hallo EA portal tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="fe6eb-130">Meer informatie over het kostenbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="fe6eb-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="fe6eb-131">Hallo met kosten schatten [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/), [totale kosten van eigendom Rekenmachine](https://aka.ms/azure-tco-calculator), en wanneer u een service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fe6eb-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="fe6eb-132">[Controleer de informatie over het gebruik en kosten regelmatig in Azure-portal](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="fe6eb-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="fe6eb-133">Schakel [Azure Advisor kosten aanbevelingen](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fe6eb-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="fe6eb-134">toolearn meer, Zie [Azure kosten management richtlijnen](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe6eb-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
