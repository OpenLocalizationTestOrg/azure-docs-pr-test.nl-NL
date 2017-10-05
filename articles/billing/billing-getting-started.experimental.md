---
title: Onverwachte kosten te voorkomen, facturerings - Azure beheren | Microsoft Docs
description: Informatie over het voorkomen van onverwachte kosten op uw Azure-factuur. Gebruik bijhouden van de kosten en beheerfuncties voor een Microsoft Azure-abonnement.
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
ms.openlocfilehash: c1185063880fa58da9487bc98977c0acae8f403d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>Onverwachte kosten met Azure-facturering en kostenbeheer voorkomen

Wanneer u zich voor Azure aanmelden, zijn er verschillende dingen die u doen kunt om een beter inzicht in uw uitgaven ophalen. De [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) een schatting van de kosten kunt opgeven voordat u een Azure-resource maakt. De [Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) biedt u de huidige verdeling van de kosten en prognose voor uw abonnement. Als u wilt groeperen en kosten voor verschillende projecten of teams begrijpen, bekijkt u [resource tagging](../azure-resource-manager/resource-group-using-tags.md). Als uw organisatie een systeem voor de rapportage die u wilt gebruiken heeft, bekijk de [facturering API's](billing-usage-rate-card-overview.md). 

U kunt ook [downloaden uit het verleden facturen en details gebruiksbestanden](billing-download-azure-invoice-daily-usage-date.md) om ervoor te zorgen dat u goed aangerekend. Zie voor meer informatie over het vergelijken van uw dagelijkse gebruik met uw factuur [inzicht in uw factuur voor Microsoft Azure](billing-understand-your-bill.md).

Als uw abonnement via een Enterprise Agreement (EA), Cloud Solution Provider (CSP) of Azure managers, geldt niet veel functies in dit artikel voor u. We hebben in plaats daarvan een andere set van hulpprogramma's die u voor het kostenbeheer van gebruiken kunt. Zie [aanvullende bronnen voor EA CSP en managers](#other-offers).

Als uw abonnement een gratis proefversie is [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO) of BizSpark, uw abonnement automatisch uitgeschakeld wanneer alle uw tegoed is gebruikt. Meer informatie over [bestedingslimieten](#spending-limit) om te voorkomen dat uw abonnement unexpectantly uitgeschakeld. 

## <a name="get-estimated-costs-before-adding-azure-services"></a>Geschatte kosten ophalen voordat u Azure-services

### <a name="estimate-cost-online-using-the-pricing-calculator"></a>Kosten online met de prijscategorie Rekenmachine schatten

Bekijk de [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) Geschatte maandelijkse kosten van de service die u geïnteresseerd bent in ophalen. U kunt een eerste partij Azure-resource als u een schatting kosten wilt toevoegen.

![Schermopname van het prijscategorie Rekenmachine-menu](./media/billing-getting-started/pricing-calc.png)

A1 Windows virtuele Machine (VM) is bijvoorbeeld geschatte kostengegevens $66.96 USD/maand in rekenuren als u de cloudservice actief laat de hele tijd:

![Schermafbeelding van de prijscategorie Rekenmachine die laat zien dat een virtuele machine van Windows A1 duurt naar 66.96 USD $ kosten per maand](./media/billing-getting-started/pricing-calcVM.png)

Zie voor meer informatie over prijzen [Veelgestelde vragen over](https://azure.microsoft.com/pricing/faq/). Of als u Neem contact op met een Azure verkoper wilt, neem dan contact op met de 1-800-867-1389.

### <a name="review-the-estimated-cost-in-the-azure-portal"></a>Bekijk de geschatte kosten in de Azure portal

Doorgaans wanneer u een service in de Azure portal toevoegt, is er een weergave waarin u een vergelijkbare geschatte kosten per maand. Bijvoorbeeld, wanneer u de grootte van uw virtuele machine van Windows kiest, ziet u de geschatte maandelijkse kosten voor de compute-uur:

![Voorbeeld: een virtuele machine van Windows A1 duurt naar 66.96 USD $ kosten per maand](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>Meldingen voor facturering instellen

Factureringsmeldingen instellen voor het ophalen van e-mailberichten wanneer uw gebruikskosten overschrijden een bedrag in dat u opgeeft. Als u maandelijks tegoed hebt, stelt u waarschuwingen voor wanneer u van een opgegeven hoeveelheid. Zie voor meer informatie [waarschuwingen voor uw Microsoft Azure-abonnementen facturering instellen](billing-set-up-alerts.md).

![Schermafbeelding van een facturering e-mailwaarschuwingen](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Deze functie is nog steeds in de preview, dus moet u het gebruik van uw regelmatig controleren.

Het is raadzaam de schatting van de kosten van de prijscategorie Rekenmachine gebruiken als uitgangspunt voor uw eerste waarschuwing.

### <a name="spending-limit"></a>Controleer of u een bestedingslimiet hebt op

Als u een abonnement dat gebruikmaakt van tegoed hebt, is klikt u vervolgens de bestedingslimiet voor u standaard ingeschakeld. Op deze manier wanneer u uw tegoed hoeven te besteden aan uw creditcard niet ophalen in rekening gebracht. Zie de [volledige lijst met Azure biedt en de beschikbaarheid van uitgavenlimiet](https://azure.microsoft.com/support/legal/offer-details/).

Echter, als u uw bestedingslimiet hebt bereikt, uw services uitgeschakeld. Dit betekent dat de toewijzing van uw virtuele machines worden opgeheven. Om te voorkomen onderhoudstijd, moet u de bestedingslimiet uitschakelen. Er wordt in rekening gebracht op uw creditcard. 

Als u hebt een uitgavenlimiet op, Ga naar de [abonnementen weergeven in het midden van het Account](https://account.windowsazure.com/Subscriptions). Een banner wordt weergegeven als uw bestedingslimiet wordt uitgevoerd op:

![Schermafbeelding van een waarschuwing over uitgaven limiet wordt op in het midden van het Account](./media/billing-getting-started/spending-limit-banner.PNG)

Klik op de banner en volg de aanwijzingen voor de bestedingslimiet verwijderen. Als u hebt niet de creditcardgegevens ingevoerd toen u zich registreerde, voert u deze als u wilt de bestedingslimiet verwijderen. Zie voor meer informatie [Azure uitgavenlimiet – hoe het werkt en hoe u kunt inschakelen of verwijderen van deze](https://azure.microsoft.com/pricing/spending-limits/).

## <a name="ways-to-monitor-your-costs-when-using-azure-services"></a>Manieren om te controleren van uw kosten wanneer u Azure-services

### <a name="tags"></a>Labels toevoegen aan uw resources voor het groeperen van je factureringsgegevens

Voor ondersteunde services kunt u codes voor een groep factureringsgegevens. Bijvoorbeeld als u meerdere virtuele machines voor verschillende teams uitvoert, kunt klikt u vervolgens u labels te categoriseren kosten door kostenplaats (uur, marketing, financiën) of de omgeving (productie, vóór productie test). 

![Schermafbeelding van instellen van de labels in de portal](./media/billing-getting-started/tags.PNG)

De labels in verschillende kosten reporting weergaven weergegeven. Bijvoorbeeld, ze zijn zichtbaar in uw [analyseweergave kosten](#costs) meteen en [toegelicht gebruik CSV](#invoice-and-usage) na de eerste factureringsperiode.

Zie voor meer informatie [met labels om uw Azure-resources te organiseren](../azure-resource-manager/resource-group-using-tags.md).

### <a name="costs"></a>Regelmatig controleren van de portal voor verdeling van de kosten en snelheid branden

Nadat u uw services die worden uitgevoerd, moet u regelmatig controleren hoeveel ze u bent kosten. U kunt zien van de huidige uitgaven en snelheid branden in Azure-portal. 

1. Ga naar de [blade abonnementen in Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en een abonnement te selecteren.

2. U moet de verdeling van de kosten zien en snelheid branden in het pop-blade. Deze wordt mogelijk niet ondersteund voor uw aanbieding (een waarschuwing wordt weergegeven boven).

    ![Schermopname van branden frequentie en de verdeling in de Azure portal](./media/billing-getting-started/burn-rate.PNG)

3. Klik op **analysis kosten** in de lijst links om te zien van de verdeling van de kosten per resource. Wacht 24 uur na het toevoegen van een service voor de gegevens zijn ingevuld.

    ![Schermafbeelding van de weergave van de kosten-analyse in Azure-portal](./media/billing-getting-started/cost-analysis.PNG)

4. U kunt filteren op andere eigenschappen zoals [labels](#tags), resourcegroep en timespan. Klik op **toepassen** om te bevestigen dat de filters en **downloaden** als u wilt de weergave exporteren naar een bestand Comma-Separated waarden (.csv).

5. Bovendien kunt u een resource voor een overzicht te besteden aan de geschiedenis en hoeveel de resourcekosten per dag.

    ![Schermafbeelding van de weergave van de geschiedenis uitgaven in Azure-portal](./media/billing-getting-started/costhistory.PNG)

Het wordt aangeraden om u te controleren of de kosten die u de schattingen die u hebt gezien ziet wanneer u de services geselecteerd. Als de kosten sterk van schattingen, Controleer de prijsstelling (A1 vs A0 VM bijvoorbeeld) die u hebt geselecteerd voor uw resources afwijken. 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Overweeg in te schakelen kostenbesparende functies zoals automatisch afsluiten voor virtuele machines

U kunt automatisch afsluiten voor uw virtuele machines in de Azure portal configureren, afhankelijk van uw scenario. Zie voor meer informatie [automatisch afsluiten voor virtuele machines met Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Schermafbeelding van de optie voor automatisch afsluiten in de portal](./media/billing-getting-started/auto-shutdown.PNG)

Automatisch afsluiten is niet hetzelfde als wanneer u binnen de virtuele machine met de opties voor energiebeheer afsluiten. Automatisch afsluiten stopt en deallocates van uw virtuele machines om te stoppen extra kosten. Zie voor meer informatie Veelgestelde vragen over de prijzen [virtuele Linux-machines](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) en [VM's van Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) over VM statussen.

Bekijk voor meer kostenbesparende functies voor uw ontwikkel- en testomgevingen, [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Inschakelen en bekijk aanbevelingen Azure Advisor te ontvangen

[Azure Advisor](../advisor/advisor-overview.md) is een preview-functie die u helpt met het vaststellen van resources met geringe gebruiksduur kosten te verlagen. Schakel deze in de Azure portal:

![Schermopname van Azure Advisor knop in Azure portal](./media/billing-getting-started/advisor-button.PNG)

Vervolgens kunt u uitvoerbare aanbevelingen krijgen in de **kosten** tabblad in het dashboard Advisor:

![Schermopname van Advisor kosten aanbeveling voorbeeld](./media/billing-getting-started/advisor-action.PNG)

Zie voor meer informatie [aanbevelingen van Advisor kosten](../advisor/advisor-cost-recommendations.md).

### <a name="billing-api"></a>Facturering-API

Onze facturering API gebruiken om op te halen programmatisch gebruiksgegevens. De API RateCard en de API-gebruik samen gebruiken om op te halen van het gebruik van uw gefactureerd. Zie voor meer informatie [inzicht in uw Microsoft Azure-brongebruik](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a>Aanvullende bronnen en bijzondere gevallen

### <a name="ea-csp-and-sponsorship-customers"></a>EA, CSP en managers klanten
Neem contact op met uw accountmanager of Azure-partner aan de slag.

| Aanbieding | Resources |
|-------------------------------|-----------------------------------------------------------------------------------|
| Enterprise Agreement (EA) | [EA portal](https://ea.azure.com/), [helpen docs](https://ea.azure.com/helpdocs), en [Power BI-rapport](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Cloud Solution Provider (CSP) | Neem contact op met uw provider |
| Azure-sponsoring | [Managers portal](https://www.microsoftazuresponsorships.com/) |

Als u beheert IT voor een grote organisatie aangeraden lezen [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) en de [enterprise IT witboek](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (download .pdf, alleen in het Engels).

### <a name="check-your-subscription-and-access"></a>Controleer uw abonnement en -toegang

Kosten weergeven vereisen [abonnementen toegang tot factureringsgegevens](billing-manage-access.md), maar alleen de accountbeheerder toegang tot de [Accountcentrum](https://account.windowsazure.com/Home/Index), factureringsgegevens wijzigen en abonnementen beheren. De accountbeheerder is de persoon die het registratieproces hebben doorlopen. Zie voor meer informatie [toevoegen of wijzigen Azure-beheerdersrollen die het abonnement of de services beheren](billing-add-change-azure-subscription-administrator.md).

Als u de accountbeheerder bent, Ga naar de [abonnementen blade in de Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en kijk in de lijst met abonnementen die u toegang tot hebt. Zoek onder **mijn rol**. Als er op het *accountbeheerder*, bent u al ok. Als er op het iets anders zoals *eigenaar*, hoeft u volledige bevoegdheden.

![Schermopname van uw rol in de weergave abonnementen in de Azure-portal](./media/billing-getting-started/sub-blade-view.PNG)

Als u niet de accountbeheerder bent, moet iemand waarschijnlijk gestuurd gedeeltelijk toegang via [toegangsbeheer op basis van een functie van Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). Voor het beheren van abonnementen en wijzig facturering info, [vinden van de accountbeheerder](billing-subscription-transfer.md#whoisaa) en vraag om de taken uitvoeren of [het abonnement aan u overdragen](billing-subscription-transfer.md).

Als uw accountbeheerder niet meer met uw organisatie is en u moet voor het beheren van facturering, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 
## <a name="need-help-contact-support"></a>Hulp nodig? Contact opnemen met ondersteuning

Als u hulp nodig hebt, moet [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.
