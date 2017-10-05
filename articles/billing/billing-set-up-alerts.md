---
title: Facturerings- of waarschuwingen voor Azure-abonnementen instellen | Microsoft Docs
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="324e5-104">Facturerings- of waarschuwingen instellen voor uw Microsoft Azure-abonnementen</span><span class="sxs-lookup"><span data-stu-id="324e5-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="324e5-105">Als u de accountbeheerder voor een Azure-abonnement bent, kunt u de Azure Billing waarschuwingsservice voor het maken van aangepaste factureringsmeldingen die u helpen controleren en beheren van facturerings activiteit voor uw Azure-accounts.</span><span class="sxs-lookup"><span data-stu-id="324e5-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="324e5-106">Deze service is in de preview, dus moet u eerst op de pagina met Preview-functies inschakelen.</span><span class="sxs-lookup"><span data-stu-id="324e5-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="324e5-107">De drempelwaarde en e-ontvangers van de waarschuwing instellen</span><span class="sxs-lookup"><span data-stu-id="324e5-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="324e5-108">Ga naar [de Preview-functies pagina](https://account.windowsazure.com/PreviewFeatures) en schakel **waarschuwingsservice facturering**.</span><span class="sxs-lookup"><span data-stu-id="324e5-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="324e5-109">Nadat u het e-mailbevestiging die de facturering-service is ingeschakeld voor uw abonnement ontvangt, gaat u naar [de pagina abonnementen](https://account.windowsazure.com/Subscriptions) in de accountportal.</span><span class="sxs-lookup"><span data-stu-id="324e5-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="324e5-110">Klik op het abonnement dat u wilt bewaken, en klik vervolgens op **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="324e5-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Schermafbeelding van de weergave abonnementen van Azure-accountcentrum, met waarschuwingen die zijn gemarkeerd][Image1]

2. <span data-ttu-id="324e5-112">Klik vervolgens op **waarschuwing toevoegen** zelf een maken.</span><span class="sxs-lookup"><span data-stu-id="324e5-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="324e5-113">U kunt een totaal van vijf factureringsmeldingen per abonnement, met een andere drempelwaarde en maximaal twee e-mailontvangers voor elke waarschuwing instellen.</span><span class="sxs-lookup"><span data-stu-id="324e5-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Schermafbeelding van de weergave van waarschuwingen, waarin u de waarschuwing kunt toevoegen][Image2]

3. <span data-ttu-id="324e5-115">Wanneer u een waarschuwing toevoegt, u een unieke naam geven, kies een bestedingslimiet drempelwaarde, en kies de e-mailadressen waarop waarschuwingen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="324e5-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="324e5-116">Wanneer de drempel instelt, kunt u ofwel een **totale facturering** of een **financieel tegoed** van de **waarschuwing voor** lijst.</span><span class="sxs-lookup"><span data-stu-id="324e5-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="324e5-117">Voor een totaal facturering, wordt een waarschuwing verzonden wanneer abonnement uitgaven de drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="324e5-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="324e5-118">Voor een financieel tegoed is een waarschuwing verzonden wanneer monetaire krediet minder wordt dan de limiet.</span><span class="sxs-lookup"><span data-stu-id="324e5-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="324e5-119">Monetaire krediet doorgaans de toepassing aan abonnementen, gratis proefversie en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="324e5-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Schermafbeelding van de weergave van waarschuwing toevoegen, waar u de geadresseerden kunt configureren][Image3]

<span data-ttu-id="324e5-121">Azure biedt ondersteuning voor elk e-mailadres, maar niet verifiëren dat de e-mailadres werken, dus Controleer voor typfouten.</span><span class="sxs-lookup"><span data-stu-id="324e5-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="324e5-122">Controleer op waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="324e5-122">Check on your alerts</span></span>
<span data-ttu-id="324e5-123">Na het instellen van waarschuwingen, wordt het Account Center vermeldt ze en toont hoe veel meer kunt u instellen.</span><span class="sxs-lookup"><span data-stu-id="324e5-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="324e5-124">Voor elke waarschuwing ziet u de datum en tijdstip van verzending, of een waarschuwing voor totale facturering of financieel tegoed is en de limiet die u instelt.</span><span class="sxs-lookup"><span data-stu-id="324e5-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="324e5-125">De datum en tijd-indeling is coördineren 24-uurs-Universal Time (UTC) en de datum is jjjj-mm-dd-indeling.</span><span class="sxs-lookup"><span data-stu-id="324e5-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="324e5-126">Klik op het plusteken voor een waarschuwing in de lijst om het te bewerken, of klik op de Prullenbak om het te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="324e5-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="324e5-127">Waarschuwingen voor facturering voor klanten met Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="324e5-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="324e5-128">EA klanten kunnen waarschuwingen krijgen voor elke afdeling onder een inschrijving door de instelling uitgaven quota's.</span><span class="sxs-lookup"><span data-stu-id="324e5-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="324e5-129">Zie [afdeling uitgaven quota](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in de portal EA aan de slag.</span><span class="sxs-lookup"><span data-stu-id="324e5-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="324e5-130">Meer informatie over het kostenbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="324e5-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="324e5-131">Geschatte kosten met behulp van de [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/), [totale kosten van eigendom Rekenmachine](https://aka.ms/azure-tco-calculator), en wanneer u een service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="324e5-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="324e5-132">[Controleer de informatie over het gebruik en kosten regelmatig in Azure-portal](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="324e5-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="324e5-133">Schakel [Azure Advisor kosten aanbevelingen](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="324e5-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="324e5-134">Zie voor meer informatie, [Azure kosten management richtlijnen](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="324e5-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
