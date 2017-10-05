---
title: Uw Azure-abonnement annuleren | Microsoft Docs
description: Hierin wordt beschreven hoe u uw Azure-abonnement, zoals de gratis proefabonnement annuleren
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a>Uw Azure-abonnement annuleren

U kunt uw Azure-abonnement als annuleren de [accountbeheerder](billing-subscription-transfer.md#whoisaa). Nadat u het abonnement annuleert, wordt uw toegang tot Azure-services en bronnen eindigt.

Voordat u uw abonnement annuleert:

* Back-up van uw gegevens. Als u gegevens in Azure storage of SQL opslaat, bijvoorbeeld een kopie downloaden. Als u een virtuele machine hebt, kunt u een afbeelding van het lokaal opslaan.
* Sluit uw services. Ga naar de [resources pagina in de beheerportal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), en **stoppen** een met virtuele machines, toepassingen of andere services.
* U kunt uw gegevens migreren. Zie [resources verplaatsen naar de nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).

Als u een betaald annuleert [Azure-ondersteuningsplan](https://azure.microsoft.com/support/plans/), u nog steeds maandelijks voor de rest van de termijn van 6 maanden wordt gefactureerd.

## <a name="cancel-subscription-using-the-azure-portal"></a>Met de Azure portal abonnement annuleren

1. Selecteer uw abonnement uit de [pagina abonnementen](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

1. Selecteer het abonnement dat u wilt annuleren en klik op **abonnement annuleren**.

    ![Schermafbeelding van de knop Annuleren](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. Volg de aanwijzingen en annulering voltooien.

## <a name="cancel-subscription-using-the-azure-account-center"></a>Met behulp van het Azure-Accountcentrum abonnement annuleren

1. Aanmelden bij de [Azure-Accountcentrum](https://account.windowsazure.com/subscriptions) als accountbeheerder.

1. Onder **klikt u op een abonnement om weer te geven informatie en gebruik**, selecteer het abonnement dat u wilt annuleren.

    ![Schermafbeelding van een voorbeeld-abonnement dat is geselecteerd](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. Selecteer aan de rechterkant van de pagina **abonnement annuleren**.

    ![Schermafbeelding van de knop Annuleren abonnement](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. Selecteer **Ja, Mijn abonnement annuleren**.

    ![Schermafbeelding van het dialoogvenster annuleren](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. Klik ![Symbool van selectievakje](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) het dialoogvenster sluiten en terug naar de abonnementpagina voor uw.

## <a name="what-happens-after-i-cancel-my-subscription"></a>Wat gebeurt er wanneer ik mijn abonnement annuleren?

Zodra u annuleert, wordt onmiddellijk facturering gestopt. Echter het kan maximaal 10 minuten duren voordat de annulering weergeven in de portal.

Daarna worden uw services uitgeschakeld. Dit betekent dat de toewijzing van uw virtuele machines worden opgeheven, tijdelijke IP-adressen worden vrijgegeven en opslag is alleen-lezen.

Tenzij u op een gratis proefversie of tegoeden heeft, bent u gefactureerd voor eventuele uitstaande gebruikskosten gegenereerd tussen de laatste factureringscyclus en de annuleringsdatum. Krijgt u de laatste factuur aan het einde van de factureringscyclus.

Nadat u uw abonnement annuleert, wachten we 90 dagen voordat uw gegevens permanent te verwijderen als u nodig hebt om deze te openen of u van gedachten verandert. We betaalt u niet voor het bewaren van gegevens. Zie voor meer informatie, [Microsoft Trust Center - hoe beheer van uw gegevens](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).

## <a name="reactivate-subscription"></a>Abonnement opnieuw activeren

Als u uw abonnement op gebruiksbasis per ongeluk annuleert, kunt u [opnieuw activeren in het midden Accounts](billing-subscription-become-disable.md).

Als uw abonnement niet betalen naar gebruik, moet u contact op met ondersteuning binnen 90 dagen na annulering uw abonnement opnieuw activeren.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.

Hebt u nog steeds vragen, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.
