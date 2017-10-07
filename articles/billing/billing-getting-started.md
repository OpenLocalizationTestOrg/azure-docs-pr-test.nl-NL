---
title: aaaPrevent onverwachte kosten facturering - Azure beheren | Microsoft Docs
description: Meer informatie over hoe tooavoid onverwachte kosten op uw Azure-factuur. Gebruik bijhouden van de kosten en beheerfuncties voor een Microsoft Azure-abonnement.
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Onverwachte kosten met Azure-facturering en kostenbeheer voorkomen

Wanneer u zich voor Azure aanmelden, zijn er verschillende dingen die u kunt doen tooget een beter inzicht in uw uitgaven. In Hallo [Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), wanneer u een abonnement hello, selecteert u kunt zien van uw huidige verdeling van de kosten en snelheid branden. U kunt ook [downloaden uit het verleden facturen en details gebruiksbestanden](billing-download-azure-invoice-daily-usage-date.md). Als u wilt dat toogroup kosten voor resources die worden gebruikt voor verschillende projecten of teams, bekijkt u [resource tagging](../azure-resource-manager/resource-group-using-tags.md). Als uw organisatie beschikt over een systeem dat u liever toouse, kijk dan eens Hallo [facturering API's](billing-usage-rate-card-overview.md). 

Zie voor meer informatie over het gebruik van uw dagelijkse [inzicht in uw factuur voor Microsoft Azure](billing-understand-your-bill.md).

Als uw abonnement via een Enterprise Agreement (EA), Cloud Solution Provider (CSP) of Azure managers is, toepassen niet veel functies in dit artikel tooyou. We hebben in plaats daarvan een andere set van hulpprogramma's die u voor het kostenbeheer van gebruiken kunt. Zie [aanvullende bronnen voor EA CSP en managers](#other-offers).

Als uw abonnement een gratis proefversie is [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO) of BizSpark, klikt u vervolgens meer informatie over [bestedingslimieten](#spending-limit) tooavoid met uw abonnement unexpectantly uitgeschakeld. 

## <a name="day-0-before-you-add-azure-services"></a>Day 0: Voordat u Azure services toevoegen

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Geschatte kosten online met behulp van Hallo prijscategorie Rekenmachine

Bekijk Hallo [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) en [totale kosten van eigendom Rekenmachine](https://aka.ms/azure-tco-calculator) tooget een schatting Hallo maandelijkse kosten van u geïnteresseerd in het bent Hallo-service. A1 Windows virtuele Machine (VM) is bijvoorbeeld geschatte toocost $66.96 USD/maand in uren compute als u het hele uitvoeringstijd Hallo laten:

![Schermopname van Hallo prijscategorie Rekenmachine aangeeft dat een A1 Windows VM geschatte toocost $66.96 USD per maand is](./media/billing-getting-started/pricing-calcVM.png)

Zie voor meer informatie [Veelgestelde vragen over prijzen](https://azure.microsoft.com/pricing/faq/). Of als u tootalk tooa persoon wilt, 1-800-867-1389 aanroepen.

### <a name="check-your-subscription-and-access"></a>Controleer uw abonnement en -toegang

Kosten weergeven vereisen [abonnementen op gebruikersniveau toobilling informatie](billing-manage-access.md), maar alleen de accountbeheerder Hallo toegang tot Hallo [Accountcentrum](https://account.windowsazure.com/Home/Index), factureringsgegevens wijzigen en abonnementen beheren. Hallo accountbeheerder is Hallo persoon die het aanmeldingsproces Hallo hebben doorlopen. Zie voor meer informatie [toevoegen of wijzigen Azure-beheerdersrollen die Hallo abonnement of services beheren](billing-add-change-azure-subscription-administrator.md).

toosee als u bent Hallo beheerder van het Account, gaat u toohello [abonnementen blade in hello Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en bekijkt hello lijst met abonnementen die u toegang tot hebt. Zoek onder **mijn rol**. Als er op het *accountbeheerder*, bent u al ok. Als er op het iets anders zoals *eigenaar*, hoeft u volledige bevoegdheden.

![Schermopname van uw rol in Hallo weergave abonnementen in hello Azure-portal](./media/billing-getting-started/sub-blade-view.PNG)

Als u bent niet de accountbeheerder hello, moet iemand waarschijnlijk gestuurd gedeeltelijk toegang via [toegangsbeheer op basis van een functie van Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage abonnementen en wijzig facturering info, [Hallo accountbeheerder vinden](billing-subscription-transfer.md#whoisaa) en vraag ze tooperform Hallo taken of [transfer Hallo abonnement tooyou](billing-subscription-transfer.md).

Als uw accountbeheerder niet meer met uw organisatie is en u toomanage financieel medewerkers moet, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 

### <a name="spending-limit"></a>Controleer of u een bestedingslimiet hebt op

Als u een abonnement dat gebruikmaakt van tegoed hebt, is klikt u vervolgens Hallo uitgavenlimiet voor u standaard ingeschakeld. Op deze manier wanneer u uw tegoed hoeven te besteden aan uw creditcard niet ophalen in rekening gebracht. Zie Hallo [volledige lijst met Azure-aanbiedingen en beschikbaarheid van uitgavenlimiet Hallo](https://azure.microsoft.com/support/legal/offer-details/).

Echter, als u uw bestedingslimiet hebt bereikt, uw services uitgeschakeld. Dit betekent dat de toewijzing van uw virtuele machines worden opgeheven. tooavoid onderhoudstijd, moet u uitschakelen Hallo uitgavenlimiet. Er wordt in rekening gebracht op uw creditcard. 

toosee als u hebt een uitgavenlimiet, gaat u toohello [abonnementen weergeven in Hallo Accountcentrum](https://account.windowsazure.com/Subscriptions). Een banner wordt weergegeven als uw bestedingslimiet wordt uitgevoerd op:

![Schermafbeelding van een waarschuwing over uitgaven limiet wordt op in het Hallo-Accountcentrum](./media/billing-getting-started/spending-limit-banner.PNG)

Klik op Hallo banner en volg de aanwijzingen tooremove Hallo uitgavenlimiet. Als u hebt niet de creditcardgegevens ingevoerd toen u zich registreerde, moet u deze tooremove Hallo uitgavenlimiet opgeven. Zie voor meer informatie [Azure uitgavenlimiet – hoe het werkt en hoe tooenable of verwijder deze](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="set-up-billing-alerts"></a>Meldingen voor facturering instellen

Stel factureringsmeldingen tooget e-mailberichten wanneer uw gebruikskosten overschrijden een bedrag in dat u opgeeft. Als u maandelijks tegoed hebt, stelt u waarschuwingen voor wanneer u van een opgegeven hoeveelheid. Zie voor meer informatie [waarschuwingen voor uw Microsoft Azure-abonnementen facturering instellen](billing-set-up-alerts.md).

![Schermafbeelding van een facturering e-mailwaarschuwingen](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Deze functie is nog steeds in de preview, dus moet u het gebruik van uw regelmatig controleren.

U kunt toouse Hallo kosten schatting van Hallo prijscalculator als uitgangspunt voor uw eerste waarschuwing.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>Limieten en quota's voor uw abonnement begrijpen

Er zijn standaardlimieten tooeach abonnement voor items zoals Hallo aantal CPU-kernen en IP-adressen. Houd ook rekening met deze limieten zijn Zie voor meer informatie [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md). U kunt een verhoging van het tooyour limiet of quota door aanvragen [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="day-1-as-you-add-services"></a>Dag 1: Als u services toevoegen

### <a name="review-hello-estimated-cost-in-hello-portal"></a>Bekijk Hallo geschatte kosten in Hallo-portal

Doorgaans wanneer u een service in Azure-portal Hallo toevoegt, is er een weergave waarin u een vergelijkbare geschatte kosten per maand. Bijvoorbeeld, wanneer u de grootte van uw virtuele machine van Windows hello kiest ziet u Hallo Geschatte maandelijkse kosten voor Hallo rekenuren:

![Voorbeeld: een A1 Windows VM is geschatte toocost $66.96 USD per maand](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>Labels tooyour resources toogroup uw factureringsgegevens toevoegen

Voor ondersteunde services kunt u codes toogroup factureringsgegevens. Bijvoorbeeld, als u meerdere virtuele machines voor verschillende teams uitvoert, kunt klikt u vervolgens u labels toocategorize kosten door kostenplaats (uur, marketing, financiën) of de omgeving (productie, vóór productie test). 

![Schermafbeelding van instellen van de labels in Hallo-portal](./media/billing-getting-started/tags.PNG)

Hallo labels worden weergegeven in verschillende kosten reporting weergaven. Bijvoorbeeld, ze zijn zichtbaar in uw [analyseweergave kosten](#costs) meteen en [toegelicht gebruik CSV](#invoice-and-usage) na de eerste factureringsperiode.

Zie voor meer informatie [Using tags tooorganize uw Azure-resources](../azure-resource-manager/resource-group-using-tags.md).

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Overweeg in te schakelen kostenbesparende functies zoals automatisch afsluiten voor virtuele machines

U kunt automatisch afsluiten voor uw virtuele machines in Azure-portal Hallo configureren, afhankelijk van uw scenario. Zie voor meer informatie [automatisch afsluiten voor virtuele machines met Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Schermafbeelding van de optie voor automatisch afsluiten in Hallo-portal](./media/billing-getting-started/auto-shutdown.PNG)

Automatisch afsluiten is niet hetzelfde zijn als bij het afsluiten binnen VM Hallo met energiebeheer Hallo. Automatisch afsluiten stopt en uw virtuele machines toostop deallocates extra kosten. Zie voor meer informatie Veelgestelde vragen over de prijzen [virtuele Linux-machines](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) en [VM's van Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) over VM statussen.

Bekijk voor meer kostenbesparende functies voor uw ontwikkel- en testomgevingen, [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

## <a name="cost-reporting"></a>Dag 2 +: Als u services, adresgebruik weergeven

### <a name="costs"></a>Regelmatig controleren Hallo-portal voor verdeling van de kosten en snelheid branden

Nadat u uw services die worden uitgevoerd, moet u regelmatig controleren hoeveel ze u bent kosten. Ziet u de huidige Hallo besteden en snelheid branden in Azure-portal. 

1. Ga naar Hallo [blade abonnementen in Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

2. Selecteer de gewenste toosee abonnement. U wellicht alleen één tooselect.

3. U moet Zie Hallo verdeling van de kosten en snelheid branden Hallo pop-blade. Deze wordt mogelijk niet ondersteund voor uw aanbieding (een waarschuwing weergegeven aan de bovenkant Hallo). Wacht 24 uur nadat u een service voor Hallo gegevens toopopulate toevoegen.
    
    ![Schermafbeelding van branden snelheid en uitsplitsing in hello Azure-portal](./media/billing-getting-started/burn-rate.PNG)

4. U kunt toopin Hallo weergave tooyour dashboard.

    ![Schermafbeelding van een weergave toohello dashboard vastmaken](./media/billing-getting-started/pin.PNG)

5. Klik op **analysis kosten** in Hallo lijst toohello links toosee Hallo verdeling van de kosten per resource.

    ![Schermopname van Hallo kosten analysis weergeven in Azure-portal](./media/billing-getting-started/cost-analysis.PNG)

6. U kunt filteren op andere eigenschappen zoals [labels](#tags), resourcegroep en timespan. Klik op **toepassen** tooconfirm Hallo filters en **downloaden** tooexport Hallo weergave tooa Comma-Separated waarden (.csv)-bestand.

7. Klik op een resource toosee te besteden aan de geschiedenis en hoeveel dit is de kosten u elke dag.

    ![Schermopname van hello te besteden aan de geschiedenis-weergave in Azure-portal](./media/billing-getting-started/costhistory.PNG)

Het wordt aangeraden om u te controleren of Hallo kosten u Hallo schattingen die werd weergegeven ziet bij het geselecteerde Hallo-services. Als er verschillen sterk Hallo kosten van de schattingen, Hallo Controleer prijsstelling (A1 vs A0 VM bijvoorbeeld) die u hebt geselecteerd voor uw resources. 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a>Kosten voor alle abonnementen in de blade facturering Hallo weergeven

Als u meerdere abonnementen beheren als accountbeheerder hello, ziet u Hallo cumulatieve factuur bedrag en uitsplitsing van uw abonnementen in Hallo [blade facturering](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade). 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Inschakelen en bekijk aanbevelingen Azure Advisor te ontvangen

[Azure Advisor](../advisor/advisor-overview.md) is een preview-functie die u helpt met het vaststellen van resources met geringe gebruiksduur kosten te verlagen. Schakel deze in hello Azure-portal:

![Schermopname van Azure Advisor knop in Azure portal](./media/billing-getting-started/advisor-button.PNG)

Vervolgens kunt u uitvoerbare aanbevelingen krijgen in Hallo **kosten** tabblad in Hallo Advisor dashboard:

![Schermopname van Advisor kosten aanbeveling voorbeeld](./media/billing-getting-started/advisor-action.PNG)

Zie voor meer informatie [aanbevelingen van Advisor kosten](../advisor/advisor-cost-recommendations.md).

### <a name="invoice-and-usage"></a>Het gebruik van uw factuur en Details ophalen nadat uw eerste factureringsperiode

U kunt uw factuur Portable Document Format (PDF) en gebruiksgegevens Comma-Separated waarden (.csv) downloaden na de eerste factureringsperiode. U kunt ook opt-in toohave uw factuur tooyou per e-mail verzonden. Deze bestanden helpen toounderstand wat uiteindelijk gefactureerd tooyou na belasting, kortingen en tegoed is. Als u niet een betaling methode gekoppeld tooyour-abonnement hebt, is het mogelijk dat deze bestanden niet beschikbaar voor u. Zie voor meer informatie [hoe tooget uw Azure-facturering factuur- en gebruiksgegevens dagelijks](billing-download-azure-invoice-daily-usage-date.md) en [inzicht in uw factuur voor Microsoft Azure](billing-understand-your-bill.md).

![Schermafbeelding van een .pdf-factuur](./media/billing-getting-started/invoice.png)

Hallo-labels die u eerder hebt ingesteld worden weergegeven in Hallo detail gebruik van CSV-bestanden:

![Schermafbeelding van labels in Hallo gebruik van CSV](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>Facturering-API

Onze facturering API tooprogrammatically get-gebruiksgegevens gebruiken. Gebruik Hallo RateCard API en Hallo gebruik API samen tooget gebruik van uw gefactureerd. Zie voor meer informatie [inzicht in uw Microsoft Azure-brongebruik](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a>Aanvullende bronnen voor EA CSP en managers

Neem contact tooyour-accountmanager of Azure-partner tooget gestart.

| Aanbieding | Resources |
|-------------------------------|-----------------------------------------------------------------------------------|
| Enterprise Agreement (EA) | [EA portal](https://ea.azure.com/), [helpen docs](https://ea.azure.com/helpdocs), en [Power BI-rapport](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Cloud Solution Provider (CSP) | Neem contact tooyour provider |
| Azure-sponsoring | [Managers portal](https://www.microsoftazuresponsorships.com/) |

Als u beheert IT voor een grote organisatie aangeraden lezen [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) en Hallo [enterprise IT witboek](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (download .pdf, alleen in het Engels).

## <a name="need-help-contact-support"></a>Hulp nodig? Contact opnemen met ondersteuning

Als u hulp nodig hebt, moet [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
