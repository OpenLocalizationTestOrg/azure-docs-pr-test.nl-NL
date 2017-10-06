---
title: aaaUnderstand uw factuur voor Azure | Microsoft Docs
description: Meer informatie over hoe tooread en inzicht in uw gebruik en de factuur voor uw Azure-abonnement
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Meer informatie over uw factuur voor Microsoft Azure
toounderstand factureren voor uw Azure, uw factuur met Hallo gedetailleerde dagelijks gebruik bestands- en kosten-rapporten in Azure-portal Hallo Hallo vergelijken.

tooobtain een PDF-bestand van uw factuur en een kopie van het gedetailleerde dagelijks gebruik bestand CSV downloaden, Zie [ophalen van uw Azure facturering facturen en dagelijks gebruiksgegevens](billing-download-azure-invoice-daily-usage-date.md). 

Zie voor gedetailleerde voorwaarden en beschrijvingen van uw factuur en gedetailleerde dagelijks gebruik bestand [begrijpen voorwaarden op uw Microsoft Azure-factuur](billing-understand-your-invoice.md) en [Understand termen in uw Microsoft Azure gedetailleerde informatie over het gebruik](billing-understand-your-usage.md). 

Zie voor meer informatie op Hallo kosten verbonden aan rapporten voor [Azure-portal kostenbeheer](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Hoe maak ik ervoor dat de kosten Hallo in mijn factuur correct zijn?
Als er een kosten op uw factuur die u op meer informatie wilt, moet u er een aantal opties zijn.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Optie 1: Uw factuur en vergelijkt u Hallo gebruiks- en kosten Hello gedetailleerde informatie over het gebruik CSV-bestand

Hallo bevat gedetailleerde informatie over het gebruik CSV-bestand uw kosten per factureringsperiode en het dagelijks gebruik. tooget gebruik van uw gedetailleerde CSV-bestand, Zie [ophalen van uw Azure facturering facturen en dagelijks gebruiksgegevens](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Uw gebruikskosten worden weergegeven op Hallo meter niveau. Hallo: volgende voorwaarden hetzelfde op beide factuur Hallo Hallo en Hallo bestand voor gedetailleerde informatie over het gebruik. Hallo facturering cyclus op Hallo factuur is bijvoorbeeld gelijkwaardige toohello factureringsperiode weergegeven in het Hallo-bestand voor gedetailleerde informatie over het gebruik.

 | Factuur (PDF) | Gedetailleerde informatie over het gebruik (CSV)|
 | --- | --- |
|Factureringscyclus | Factureringsperiode |
 |Naam |De categorie van de meter |
 |Type |De subcategorie meter |
 |Resource |De naam van de meter |
 |Regio |De regio van de meter |
 |Verbruikt |Verbruikt aantal |
 |Inbegrepen |Inbegrepen hoeveelheid |
 |Factureerbaar |Overschreden hoeveelheid |

Hallo **gebruikskosten** sectie van uw factuur heeft een totale waarde Hallo voor elke meter die is gebruikt tijdens de factureringsperiode. Hallo ziet volgende schermafbeelding u bijvoorbeeld een usage-kosten voor hello Azure Scheduler-service.

![Factuur gebruikskosten](./media/billing-understand-your-bill/1.png)

Hallo **instructie** sectie van de gedetailleerde informatie over het gebruik CSV Hallo toont dezelfde kosten. Beide Hallo *verbruikt* bedrag en *waarde* overeen Hallo factuur.

![CSV-gebruikskosten](./media/billing-understand-your-bill/2.png)

een verdeling van deze kosten per dag, Ga toohello toosee **dagelijkse gebruik** sectie Hallo CSV. Filteren op 'Scheduler' onder *Meter categorie* en kunt u zien welke Hallo dagen meter gebruikt en hoeveel is verbruikt. Hallo *Resource* en *resourcegroep* informatie is ook vermeld voor vergelijking. Hallo *verbruikt* waarden moeten optellen van toowhat op Hallo factuur weergegeven.

![Sectie van de dagelijkse gebruik in Hallo CSV](./media/billing-understand-your-bill/3.png)

tooget hello kosten per dag, Vermenigvuldig Hallo *verbruikt* bedragen Hello *snelheid* waarde van Hallo **instructie** sectie.

toolearn meer informatie over het Hallo-factuur, Zie [inzicht in uw Azure-factuur](billing-understand-your-invoice.md).

toolearn over elk van de kolommen Hallo in Hallo CSV, Zie [inzicht in het gebruik van uw Azure gedetailleerde](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Optie 2: Uw factuur en vergelijken met de Hallo gebruiks- en kosten in hello Azure-portal

Hello Azure-portal kunt u controleren of uw kosten. Hello Azure-portal biedt kosten management grafieken voor een snel overzicht van uw gebruik en Hallo kosten op uw factuur.

toocontinue Hallo-voorbeeld uit het bovenstaande bezoeken Hallo [pagina abonnementen](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), selecteer uw abonnement en kies vervolgens **analysis kosten**. U kunt daar Hallo tijdsspanne opgeven en Zie informatie over het gebruik in rekening gebracht voor hello Azure Scheduler-service.

![Analyse van kosten weergeven in Azure-portal](./media/billing-understand-your-bill/4.png)

toosee hello dag kosten opgesplitst in **kosten geschiedenis**, klikt u op Hallo rij.

![Kosten geschiedenis-weergave in Azure-portal](./media/billing-understand-your-bill/5.png)

toolearn meer, Zie [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](billing-getting-started.md#costs).

## <a name="external"></a>Hoe zit het met externe servicekosten?
Externe services (ook wel bekend als Azure Marketplace orders) worden geleverd door onafhankelijke serviceleveranciers en worden afzonderlijk gefactureerd. Hallo kosten worden niet weergegeven op uw Azure-factuur. toolearn meer, Zie [inzicht in uw Azure externe servicekosten](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Hoe maak ik een betaling?

Als u een creditcard of een betaalpas als uw betalingsmethode instellen, Hallo betaling is in rekening gebracht automatisch binnen tien dagen na afloop van de factureringsperiode Hallo. Op uw creditcard-instructie Hallo regelitem zou spreken **MSFT Azure**.

Als u [betaalde door facturering](billing-how-to-pay-by-invoice.md), de locatie van uw betaling toohello vermeld onder Hallo van uw factuur verzenden. Voor meer informatie [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Hoe kan ik Hallo status van een betaling van creditcard controleren?

[Maak een ondersteuningsticket](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask Hallo status van uw betaling. 

## <a name="tips-for-cost-management"></a>Tips voor het kostenbeheer van
- Kosten schatten met behulp van Hallo [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) en [totale kosten van eigendom Rekenmachine](https://aka.ms/azure-tco-calculator), en krijgt u Hallo [gedetailleerde prijsinformatie voor elke service](https://azure.microsoft.com/en-us/pricing/).
- [Instellen van waarschuwingen facturering](billing-set-up-alerts.md).
- [Controleer de informatie over het gebruik en kosten regelmatig in hello Azure-portal](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.

Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
