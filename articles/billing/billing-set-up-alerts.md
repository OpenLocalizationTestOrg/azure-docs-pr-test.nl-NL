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
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Facturerings- of waarschuwingen instellen voor uw Microsoft Azure-abonnementen
Als u Hallo beheerder van het Account voor een Azure-abonnement bent, kunt u hello Azure Billing waarschuwingsservice toocreate aangepast facturering waarschuwingen die helpen u te bewaken en beheren van activiteit facturering voor uw Azure-accounts.

Deze service is in de preview, dus u tooenable het Hallo Voorbeeldfuncties pagina eerst moet.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Hallo drempelwaarde en e-mail ontvangers instellen
1. Ga naar [Hallo Voorbeeldfuncties pagina](https://account.windowsazure.com/PreviewFeatures) en schakel **waarschuwingsservice facturering**.

1. Nadat u Hallo e-mailbevestiging die facturering Hallo-service is ingeschakeld voor uw abonnement ontvangt, gaat u naar [Hallo abonnementen pagina](https://account.windowsazure.com/Subscriptions) in Hallo-accountportal. Klik op Hallo abonnement u wilt toomonitor en klik vervolgens op **waarschuwingen**.

    ![Schermafbeelding van de weergave van de abonnementen Hallo van Azure-accountcentrum, met waarschuwingen die zijn gemarkeerd][Image1]

2. Klik vervolgens op **waarschuwing toevoegen** toocreate zelf een. U kunt een totaal van vijf factureringsmeldingen per abonnement, met een andere drempelwaarde en omhoog in de e-mailontvangers tootwo voor elke waarschuwing instellen.

    ![Schermopname van Hallo waarschuwingen weergeven, waarin u de waarschuwing kunt toevoegen][Image2]

3. Wanneer u een waarschuwing toevoegt, u een unieke naam geven, kies een bestedingslimiet drempelwaarde en kies Hallo e-mailadressen waarop waarschuwingen worden verzonden. Bij het instellen van Hallo drempelwaarde, kunt u ofwel een **totale facturering** of een **financieel tegoed** van Hallo **waarschuwing voor** lijst. Voor een totaal facturering, wordt een waarschuwing verzonden wanneer Hallo abonnement uitgaven overschrijdt. Voor een financieel tegoed is een waarschuwing verzonden wanneer monetaire krediet Hallo limiet beneden. Monetaire krediet doorgaans tooFree proefversie en Visual Studio-abonnementen van toepassing.

    ![Schermopname van Hallo waarschuwing toevoeging weergave, waar u de geadresseerden kunt configureren][Image3]

Azure biedt ondersteuning voor elk e-mailadres, maar niet controleren of de e-mailadres Hallo werkt, dus Controleer op typefouten.

## <a name="check-on-your-alerts"></a>Controleer op waarschuwingen
Na het instellen van waarschuwingen, bevat deze hello Accountcentrum- en ziet u hoe veel meer kunt u instellen. Voor elke waarschuwing ziet u Hallo datum en tijdstip van verzending, of het om een waarschuwing voor totale facturering of financieel tegoed en Hallo limiet die u instelt. Hallo datum- en tijdnotatie is coördineren 24-uurs-Universal Time (UTC) en Hallo datum is jjjj-mm-dd-indeling. Klik op Hallo plus ondertekenen voor een waarschuwing in Hallo lijst tooedit of Hallo-Prullenbak toodelete deze.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Waarschuwingen voor facturering voor klanten met Enterprise Agreement (EA)
EA klanten kunnen waarschuwingen krijgen voor elke afdeling onder een inschrijving door de instelling uitgaven quota's. Zie [afdeling uitgaven quota](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in Hallo EA portal tooget gestart.

## <a name="learn-more-about-azure-cost-management"></a>Meer informatie over het kostenbeheer van Azure
- Hallo met kosten schatten [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/), [totale kosten van eigendom Rekenmachine](https://aka.ms/azure-tco-calculator), en wanneer u een service toevoegen.
- [Controleer de informatie over het gebruik en kosten regelmatig in Azure-portal](billing-getting-started.md#costs).
- Schakel [Azure Advisor kosten aanbevelingen](../advisor/advisor-cost-recommendations.md).

toolearn meer, Zie [Azure kosten management richtlijnen](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
