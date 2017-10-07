---
title: aaaProvide contact op met informatie over de beveiliging in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe tooprovide beveiliging contact op met de details in Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="0622c-103">Neem contact op met informatie over de beveiliging in Azure Security Center bieden</span><span class="sxs-lookup"><span data-stu-id="0622c-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="0622c-104">Azure Security Center wordt het beste contact op met informatie over de beveiliging voor uw Azure-abonnement te leveren als u dat nog niet gedaan hebt.</span><span class="sxs-lookup"><span data-stu-id="0622c-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="0622c-105">Deze informatie wordt gebruikt door Microsoft toocontact of Hallo Microsoft Security Response Center (MSRC) detecteert dat uw klantgegevens is geopend door een onrechtmatig of niet-geautoriseerde partij.</span><span class="sxs-lookup"><span data-stu-id="0622c-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="0622c-106">MSRC voert selecteert u beveiliging hello Azure-netwerk en infrastructuur bewaken en threat intelligence en misbruik klachten ontvangt van een derde partij.</span><span class="sxs-lookup"><span data-stu-id="0622c-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="0622c-107">Een e-mailmelding wordt verzonden op Hallo eerste dagelijkse exemplaar van een waarschuwing en alleen voor waarschuwingen met hoog dreigingsniveau.</span><span class="sxs-lookup"><span data-stu-id="0622c-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="0622c-108">E-mailvoorkeuren kunnen alleen worden geconfigureerd voor abonnementsbeleid.</span><span class="sxs-lookup"><span data-stu-id="0622c-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="0622c-109">Deze instellingen worden overgenomen door resourcegroepen binnen een abonnement.</span><span class="sxs-lookup"><span data-stu-id="0622c-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="0622c-110">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="0622c-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="0622c-111">Dit is geen stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="0622c-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="0622c-112">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="0622c-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="0622c-113">In Hallo **aanbevelingen** blade Selecteer **contact op met informatie over de beveiliging bieden**.</span><span class="sxs-lookup"><span data-stu-id="0622c-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="0622c-114">![Neem contact op met beveiliging bieden][1]</span><span class="sxs-lookup"><span data-stu-id="0622c-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="0622c-115">Hiermee opent u de blade Hallo **contact op met informatie over de beveiliging bieden**.</span><span class="sxs-lookup"><span data-stu-id="0622c-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="0622c-116">Selecteer hello Azure-abonnement tooprovide contactgegevens op.</span><span class="sxs-lookup"><span data-stu-id="0622c-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="0622c-117">![Contactgegevens voor beveiliging verstrekken][2]</span><span class="sxs-lookup"><span data-stu-id="0622c-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="0622c-118">Een tweede **contact op met informatie over de beveiliging bieden** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="0622c-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="0622c-119">Voer Hallo beveiliging contact op met e-mailadres of adressen gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="0622c-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="0622c-120">Er is geen limiet toohello getal met e-mailadressen die u kunt invoeren.</span><span class="sxs-lookup"><span data-stu-id="0622c-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="0622c-121">Geef één beveiliging contact op met internationaal telefoonnummer.</span><span class="sxs-lookup"><span data-stu-id="0622c-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="0622c-122">tooreceive e-mailberichten over waarschuwingen met hoog dreigingsniveau, schakel de optie Hallo **Stuur mij e-mails over waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="0622c-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="0622c-123">In toekomstige hello hebt u Hallo optie toosend e meldingen toosubscription eigenaren.</span><span class="sxs-lookup"><span data-stu-id="0622c-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="0622c-124">Deze optie is momenteel grijs weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0622c-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="0622c-125">Selecteer **OK** tooapply Hallo beveiliging contact opnemen met informatie tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="0622c-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="0622c-126">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0622c-126">See also</span></span>
<span data-ttu-id="0622c-127">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="0622c-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="0622c-128">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="0622c-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0622c-129">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="0622c-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="0622c-130">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="0622c-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="0622c-131">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="0622c-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="0622c-132">[Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="0622c-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="0622c-133">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="0622c-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="0622c-134">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Hallo nieuwste Azure-beveiliging nieuws en informatie.</span><span class="sxs-lookup"><span data-stu-id="0622c-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
