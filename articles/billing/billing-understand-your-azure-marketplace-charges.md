---
title: Inzicht in uw Azure externe servicekosten | Microsoft Docs
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
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="94b49-103">Inzicht in uw Azure-facturering voor de externe service kosten</span><span class="sxs-lookup"><span data-stu-id="94b49-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="94b49-104">Externe services gebruikt voor Azure Marketplace worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="94b49-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="94b49-105">In het algemeen zijn gepubliceerd door andere leveranciers beschikbaar voor Azure services maar volledig zijn geïntegreerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="94b49-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="94b49-106">ClearDB en SendGrid zijn bijvoorbeeld externe services die u in Azure kunt aanschaffen, maar niet zijn gepubliceerd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94b49-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="94b49-107">Wanneer u een nieuwe externe service of de resource inricht, wordt een waarschuwing weergegeven:</span><span class="sxs-lookup"><span data-stu-id="94b49-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Marketplace kopen waarschuwing](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="94b49-109">Externe services zijn gepubliceerd door bedrijven die geen Microsoft, maar soms ook Microsoft-producten zijn aangemerkt als externe services.</span><span class="sxs-lookup"><span data-stu-id="94b49-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="94b49-110">Hoe externe services worden gefactureerd</span><span class="sxs-lookup"><span data-stu-id="94b49-110">How external services are billed</span></span>
- <span data-ttu-id="94b49-111">Externe services worden afzonderlijk gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="94b49-111">External services are billed separately.</span></span> <span data-ttu-id="94b49-112">Ze worden behandeld als afzonderlijke orders binnen uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="94b49-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="94b49-113">De factureringsperiode voor elke service is ingesteld bij de aankoop van de service.</span><span class="sxs-lookup"><span data-stu-id="94b49-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="94b49-114">Niet te verwarren met de factureringsperiode van het abonnement waaronder u die hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="94b49-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="94b49-115">U krijgt ook afzonderlijk facturen en uw creditcard wordt afzonderlijk in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="94b49-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="94b49-116">Elke externe service heeft een ander facturering model.</span><span class="sxs-lookup"><span data-stu-id="94b49-116">Each external service has a different billing model.</span></span> <span data-ttu-id="94b49-117">Sommige services worden gefactureerd op betalen naar gebruik wijze bij anderen gebruik maken van een maandelijkse gebaseerde betaling-model.</span><span class="sxs-lookup"><span data-stu-id="94b49-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="94b49-118">Hebt u een creditcard nodig voor de externe Azure-services, kan niet het kopen van externe services met factuur betalen.</span><span class="sxs-lookup"><span data-stu-id="94b49-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="94b49-119">U kunt maandelijks gratis tegoed niet gebruiken voor externe services.</span><span class="sxs-lookup"><span data-stu-id="94b49-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="94b49-120">Als u een Azure-abonnement met [gratis tegoed](https://azure.microsoft.com/pricing/spending-limits/), ze kunnen niet worden toegepast op de externe service facturen.</span><span class="sxs-lookup"><span data-stu-id="94b49-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="94b49-121">Een creditcard gebruiken voor de aanschaf van externe services.</span><span class="sxs-lookup"><span data-stu-id="94b49-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="94b49-122">Weergave externe service uitgaven en geschiedenis in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="94b49-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="94b49-123">U kunt een lijst weergeven met de externe services die zich op elk abonnement binnen de [Azure-portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="94b49-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="94b49-124">Aanmelden bij de [Azure-portal](https://portal.azure.com/) als de accountbeheerder.</span><span class="sxs-lookup"><span data-stu-id="94b49-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="94b49-125">Selecteer in het menu Hub **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="94b49-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Selecteer de abonnementen in het Hub-menu](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="94b49-127">In de **abonnementen** blade, selecteer het abonnement dat u wilt weergeven en selecteer vervolgens **externe services**.</span><span class="sxs-lookup"><span data-stu-id="94b49-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Selecteer een abonnement op de blade facturering](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="94b49-129">U ziet elk van uw bestellingen externe service, de naam van uitgever, servicelaag die u hebt aangeschaft, hebt u de bron en de status van de huidige gegeven naam.</span><span class="sxs-lookup"><span data-stu-id="94b49-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="94b49-130">Om te zien voorbij facturen, selecteert u een externe service.</span><span class="sxs-lookup"><span data-stu-id="94b49-130">To see past bills, select an external service.</span></span>
   
    ![Selecteer een externe service](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="94b49-132">Hier kunt u weergeven uit het verleden factuur bedragen, met inbegrip van de btw-verdeling.</span><span class="sxs-lookup"><span data-stu-id="94b49-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Weergave van de externe services factureringsgeschiedenis](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="94b49-134">Weergave van de externe service uitgaven voor klanten met Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="94b49-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="94b49-135">EA klanten kunnen zien van de externe service uitgaven en rapporten in de portal EA downloaden.</span><span class="sxs-lookup"><span data-stu-id="94b49-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="94b49-136">Zie [Azure Marketplace voor EA klanten](https://ea.azure.com/helpdocs/azureMarketplace) aan de slag.</span><span class="sxs-lookup"><span data-stu-id="94b49-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="94b49-137">Betalingswijzen voor externe serviceorders beheren</span><span class="sxs-lookup"><span data-stu-id="94b49-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="94b49-138">Uw betaling updatemethoden voor de externe serviceorders uit de [Accountcentrum](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="94b49-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="94b49-139">Als u uw abonnement met een werk of School-account hebt gekocht [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) wijzigingen aanbrengen in uw betalingswijze.</span><span class="sxs-lookup"><span data-stu-id="94b49-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="94b49-140">Aanmelden bij de [Accountcentrum](https://account.windowsazure.com/) en [gaat u naar de **marketplace** tabblad](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="94b49-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Selecteer marketplace in het midden van het account](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="94b49-142">Selecteer de externe service die u wilt beheren</span><span class="sxs-lookup"><span data-stu-id="94b49-142">Select the external service you want to manage</span></span>
   
    ![Selecteer de externe service die u wilt beheren](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="94b49-144">Klik op **betalingsmethode wijzigen** aan de rechterkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="94b49-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="94b49-145">Deze koppeling keert u terug naar een andere portal voor het beheren van uw betalingswijze.</span><span class="sxs-lookup"><span data-stu-id="94b49-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Volgorde-samenvatting](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="94b49-147">Klik op **info bewerken** en volg de instructies voor het bijwerken van uw betalingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="94b49-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Selecteer Bewerken info](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="94b49-149">Een externe serviceorder annuleren</span><span class="sxs-lookup"><span data-stu-id="94b49-149">Cancel an external service order</span></span>
<span data-ttu-id="94b49-150">Als u uw externe service bestelling annuleert wilt, verwijdert u de resource in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94b49-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Bron verwijderen](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="94b49-152">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="94b49-152">Need help?</span></span> <span data-ttu-id="94b49-153">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="94b49-153">Contact support.</span></span>
<span data-ttu-id="94b49-154">Hebt u nog steeds vragen, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="94b49-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

