---
title: aaaUnderstand de externe Azure servicekosten | Microsoft Docs
description: Meer informatie over de facturering van externe services, voorheen bekend als Marketplace, kosten in Azure.
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="6b243-103">Inzicht in uw Azure-facturering voor de externe service kosten</span><span class="sxs-lookup"><span data-stu-id="6b243-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="6b243-104">Externe services gebruikt toobe aangeroepen Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6b243-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="6b243-105">In het algemeen zijn gepubliceerd door andere leveranciers beschikbaar voor Azure services maar volledig zijn geïntegreerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b243-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="6b243-106">ClearDB en SendGrid zijn bijvoorbeeld externe services die u in Azure kunt aanschaffen, maar niet zijn gepubliceerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6b243-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="6b243-107">Wanneer u een nieuwe externe service of de resource inricht, wordt een waarschuwing weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6b243-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Marketplace kopen waarschuwing](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="6b243-109">Externe services zijn gepubliceerd door bedrijven die geen Microsoft, maar soms ook Microsoft-producten zijn aangemerkt als externe services.</span><span class="sxs-lookup"><span data-stu-id="6b243-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="6b243-110">Hoe externe services worden gefactureerd</span><span class="sxs-lookup"><span data-stu-id="6b243-110">How external services are billed</span></span>
- <span data-ttu-id="6b243-111">Externe services worden afzonderlijk gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="6b243-111">External services are billed separately.</span></span> <span data-ttu-id="6b243-112">Ze worden behandeld als afzonderlijke orders binnen uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6b243-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="6b243-113">Hallo factureringsperiode voor elke service is ingesteld bij de aankoop van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6b243-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="6b243-114">Niet toobe verward met Hallo factureringsperiode van Hallo abonnement waaronder u die hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="6b243-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="6b243-115">U krijgt ook afzonderlijk facturen en uw creditcard wordt afzonderlijk in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="6b243-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="6b243-116">Elke externe service heeft een ander facturering model.</span><span class="sxs-lookup"><span data-stu-id="6b243-116">Each external service has a different billing model.</span></span> <span data-ttu-id="6b243-117">Sommige services worden gefactureerd op betalen naar gebruik wijze bij anderen gebruik maken van een maandelijkse gebaseerde betaling-model.</span><span class="sxs-lookup"><span data-stu-id="6b243-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="6b243-118">Hebt u een creditcard nodig voor de externe Azure-services, kan niet het kopen van externe services met factuur betalen.</span><span class="sxs-lookup"><span data-stu-id="6b243-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="6b243-119">U kunt maandelijks gratis tegoed niet gebruiken voor externe services.</span><span class="sxs-lookup"><span data-stu-id="6b243-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="6b243-120">Als u een Azure-abonnement met [gratis tegoed](https://azure.microsoft.com/pricing/spending-limits/), ze niet kunnen worden toegepast tooexternal service facturen.</span><span class="sxs-lookup"><span data-stu-id="6b243-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="6b243-121">Een creditcard toopurchase externe services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b243-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="6b243-122">Weergave externe service uitgaven en geschiedenis in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6b243-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="6b243-123">U kunt een lijst weergeven met Hallo externe services die zich op elk abonnement binnen Hallo [Azure-portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="6b243-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="6b243-124">Meld u aan toohello [Azure-portal](https://portal.azure.com/) als accountbeheerder Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b243-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="6b243-125">Selecteer in het menu Hub Hallo **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="6b243-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Selecteer abonnementen in het Hub-menu Hallo](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="6b243-127">In Hallo **abonnementen** blade, selecteer Hallo-abonnement dat u tooview wilt en selecteer vervolgens **externe services**.</span><span class="sxs-lookup"><span data-stu-id="6b243-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Selecteer een abonnement op Hallo facturering blade](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="6b243-129">U kunt elk van de externe serviceorders, Hallo uitgeversnaam, servicelaag die u hebt aangeschaft, naam die u hebt opgegeven Hallo bron en de huidige status Hallo moeten zien.</span><span class="sxs-lookup"><span data-stu-id="6b243-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="6b243-130">toosee voorbij rekeningen, selecteert u een externe service.</span><span class="sxs-lookup"><span data-stu-id="6b243-130">toosee past bills, select an external service.</span></span>
   
    ![Selecteer een externe service](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="6b243-132">Hier kunt u het verleden factuur bedragen, met inbegrip van Hallo btw verdeling weergeven.</span><span class="sxs-lookup"><span data-stu-id="6b243-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![Weergave van de externe services factureringsgeschiedenis](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="6b243-134">Weergave van de externe service uitgaven voor klanten met Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="6b243-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="6b243-135">EA klanten kunnen zien van de externe service uitgaven en rapporten in Hallo EA portal downloaden.</span><span class="sxs-lookup"><span data-stu-id="6b243-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="6b243-136">Zie [Azure Marketplace voor EA klanten](https://ea.azure.com/helpdocs/azureMarketplace) tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="6b243-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="6b243-137">Betalingswijzen voor externe serviceorders beheren</span><span class="sxs-lookup"><span data-stu-id="6b243-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="6b243-138">Uw betaling updatemethoden voor externe serviceorders van Hallo [Accountcentrum](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="6b243-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="6b243-139">Als u uw abonnement met een werk of School-account hebt gekocht [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake tooyour betalingsmethode wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6b243-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="6b243-140">Meld u aan toohello [Accountcentrum](https://account.windowsazure.com/) en [navigeren toohello **marketplace** tabblad](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="6b243-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Selecteer marketplace in Hallo account center](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="6b243-142">Selecteer de externe service Hallo gewenste toomanage</span><span class="sxs-lookup"><span data-stu-id="6b243-142">Select hello external service you want toomanage</span></span>
   
    ![Selecteer de externe service Hallo gewenste toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="6b243-144">Klik op **betalingsmethode wijzigen** aan de rechterkant Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="6b243-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="6b243-145">Deze koppeling brengt u tooa verschillende portal toomanage uw betalingswijze.</span><span class="sxs-lookup"><span data-stu-id="6b243-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![Volgorde-samenvatting](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="6b243-147">Klik op **info bewerken** en volg de instructies tooupdate uw betalingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="6b243-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![Selecteer Bewerken info](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="6b243-149">Een externe serviceorder annuleren</span><span class="sxs-lookup"><span data-stu-id="6b243-149">Cancel an external service order</span></span>
<span data-ttu-id="6b243-150">Als u uw bestelling externe service toocancel wilt, Hallo resource in Hallo verwijderen [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b243-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![Bron verwijderen](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="6b243-152">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="6b243-152">Need help?</span></span> <span data-ttu-id="6b243-153">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="6b243-153">Contact support.</span></span>
<span data-ttu-id="6b243-154">Hebt u nog steeds vragen, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="6b243-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

