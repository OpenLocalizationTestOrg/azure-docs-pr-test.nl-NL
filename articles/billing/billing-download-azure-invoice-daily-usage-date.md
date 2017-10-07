---
title: aaaDownload Azure facturen en dagelijks gebruik factureringsgegevens | Microsoft Docs
description: Beschrijft hoe toodownload of weergave uw Azure-facturering factuur- en gebruiksgegevens dagelijks.
keywords: factuur, factuur downloaden, azure factuur, azure gebruik
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Downloaden of uw Azure-factuur en de dagelijkse gebruiksgegevens weergeven
U kunt uw factuur downloaden van Hallo [Azure-portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) of wordt verzonden in e-mailbericht. toodownload uw dagelijkse gebruik, Ga toohello [Azure-Accountcentrum](https://account.windowsazure.com). Alleen bepaalde functies hebben een machtiging tooget factuurgegevens factuur en gebruik, zoals Hallo accountbeheerder. toolearn meer informatie over het verkrijgen van toegang toobilling informatie, Zie [beheren toegang tooAzure facturering rollen](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Uw factuur ophalen in e-mailbericht (PDF)
U kunt opt-in en configureert extra ontvangers tooreceive uw Azure-factuur in een e-mailbericht. Deze functie is mogelijk niet beschikbaar voor bepaalde abonnementen zoals ondersteuning biedt, Enterprise overeenkomsten of Azure in Open.

1. Selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Aanmelden voor elk abonnement dat u bezit. Klik op **facturen** vervolgens **e-mijn factuur**. 

    ![Schermafbeelding van Hallo opt-in stroom](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Klik op **Opt-in** Hallo voorwaarden en accepteren.

    ![Schermafbeelding van Hallo opt-in stroom](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Nadat u Hallo overeenkomst hebt geaccepteerd, kunt u extra ontvangers configureren.

    ![Schermafbeelding van Hallo opt-in stroom](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Als u een e-mailbericht geen krijgt nadat Hallo stappen hebt uitgevoerd, controleert u of uw e-mailadres klopt in Hallo [communicatievoorkeuren in uw profiel](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Facturen downloaden vanuit Azure-portal (PDF)

1. Selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal als [een gebruiker met toegang tooinvoices](billing-manage-access.md).

2. Selecteer **facturen**. 

    ![Schermafbeelding van Hallo facturering en gebruik de optie](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Klik op **factuur downloaden** tooview een kopie van uw factuur PDF. Als er op het **niet beschikbaar**, Zie [waarom zie ik niet een factuur voor Hallo laatste factureringsperiode?](#noinvoice)

    ![Schermafbeelding van facturering perioden, opties voor het downloaden van Hallo en totale kosten voor elke factureringsperiode](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. U kunt ook het gebruik van uw dagelijkse weergeven door te klikken op Hallo factureringsperiode. 

Zie voor meer informatie over uw factuur [inzicht in uw factuur voor Microsoft Azure](billing-understand-your-bill.md). Zie voor meer informatie over het beheren van kosten [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Informatie over het gebruik van Hallo Accountcentrum (.csv) downloaden

1. Meld u aan bij Hallo [Azure-Accountcentrum](https://account.windowsazure.com/subscriptions) als accountbeheerder Hallo.

2. Hallo-abonnement waarvoor u informatie over de factuur en informatie over het gebruik van Hallo wilt selecteren.

3. Selecteer **facturering geschiedenis**. 

    ![Schermafbeelding van de optie factureren geschiedenis](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Hier ziet u de instructies voor Hallo laatste zes facturering periodes en Hallo huidige gefactureerd periode. 

    ![Schermafbeelding van facturering perioden, opties toodownload factuur en dagelijkse gebruik en totale kosten voor elke factureringsperiode](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Selecteer **weergave huidige instructie** toosee een schatting maken van uw kosten op Hallo tijd Hallo schatting is gegenereerd. Deze informatie wordt alleen dagelijks bijgewerkt en kan niet alle gebruik van uw bevatten. Uw maandelijkse factuur kan afwijken van deze schatting.

    ![Schermafbeelding van Hallo weergave huidige instructie optie](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Schermafbeelding van Hallo schatting van de huidige kosten](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Selecteer **gebruiksgegevens downloaden** toodownload Hallo dagelijkse gegevens over het gebruik als een CSV-bestand. Als er twee versies beschikbaar zijn, wordt versie 2 downloaden.

    ![Schermafbeelding van Hallo gebruiksgegevens downloaden optie](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Alleen Hallo accountbeheerder toegang tot hello Azure-Accountcentrum. Andere facturering beheerders, zoals een eigenaar krijgt Hallo met informatie over het gebruik [facturering API's](billing-usage-rate-card-overview.md).

Zie voor meer informatie over het gebruik van uw dagelijkse [inzicht in uw factuur voor Microsoft Azure](billing-understand-your-bill.md). Zie voor meer informatie over het beheren van kosten [te voorkomen dat onverwachte kosten met Azure-facturering en kostenbeheer](billing-getting-started.md).

## <a name="noinvoice"></a>Waarom zie ik niet een factuur voor Hallo laatste factureringsperiode?

Er zijn diverse redenen dat een factuur niet wordt weergegeven:

- U hebt een maandbedrag tegoed bij uw abonnement die u hebt niet langer zijn dan of u hebt een gratis proefversie. Een factuur wordt alleen gegenereerd wanneer u geld verschuldigd bent.

- Het is minder dan 30 dagen na Hallo die u tooAzure geabonneerd.

- Hallo factuur niet is nog gegenereerd. Wachten tot het einde van de factureringsperiode Hallo Hallo.

- Als u niet Hallo accountbeheerder bent mogelijk ouder facturen avaialbe tooyou niet.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog steeds meer vragen hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.

