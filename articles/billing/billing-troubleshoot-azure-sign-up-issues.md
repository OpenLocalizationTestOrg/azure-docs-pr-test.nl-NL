---
title: aaaTroubleshoot Azure aanmelding oplossen | Microsoft Docs
description: Hierin wordt beschreven hoe tootroubleshoot enkele algemene Azure aanmelden problemen.
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Problemen oplossen van problemen met aanmelding voor Azure
Als u niet kunt voor Azure aanmelden, gebruikt u Hallo tips in dit artikel tootroubleshoot veelvoorkomende problemen. Als er een probleem met je creditcard tijdens het aanmelden, Zie [uw betaalpas of creditcard is afgewezen op Azure aanmelding](billing-credit-card-fails-during-azure-sign-up.md). Als u Azure-account hebt, maar u kunt zich niet aanmelden, Zie [ik niet aanmelden toomanage mijn Azure-abonnement](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>De voortgangsbalk reageert niet meer in de sectie 'Identiteitscontrole door kaart'

Hallo identiteitscontrole toocomplete door kaart, cookies van derden moeten worden toegestaan voor uw browser.

![Schermopname van Hallo identiteitscontrole voor kaart sectie verkeerd-om tijdens de registratie](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Volgende stappen tooupdate Hallo cookie-instellingen van uw browser gebruiken.

1. Als u Chrome, gaat u verder te**instellingen** > **weergeven geavanceerde instellingen** > **Privacy** > **inhoud instellingen**. Schakel het selectievakje **blokkeren van cookies van derden en sitegegevens**.
2. Als u Edge gebruikt, gaat u verder te**instellingen** > **weergave geavanceerde instellingen** > **Cookies**. Selecteer **geen cookies blokkeren**.
3. Hello Azure aanmeldpagina vernieuwen en controleer of Hallo probleem is opgelost.
4. Als Hallo vernieuwen niet Hallo probleem is opgelost, sluit af en start de browser opnieuw en probeer het opnieuw.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Creditcardformulier biedt geen ondersteuning voor Mijn factuuradres
Je factuuradres moet toobe in Hallo land die u hebt geselecteerd in Hallo **over u** sectie. Zorg ervoor dat u de juiste land Hallo selecteren.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Er is geen SMS-berichten of aanroepen tijdens de registratie accountverificatie
Het is meestal veel sneller, kan het verificatie code toobe bezorgd toofour minuten duren. Hallo telefoonnummer op dat die u voor de verificatie invoert is niet opgeslagen als een telefoonnummer voor Hallo-account.

Hier volgen enkele aanvullende tips:
* Een VOIP-telefoonnummer kan niet worden gebruikt voor de verificatieprocedure Hallo.
* Controleer u invoert, met inbegrip van Hallo-landcode die u hebt geselecteerd in het vervolgkeuzemenu Hallo Hallo telefoonnummer.
* Als uw telefoon geen tekstberichten (SMS) ontvangt, probeert u Hallo **Bel me** optie.
* Zorg ervoor dat uw telefoon aanroepen of SMS-berichten van een getal van de Verenigde Staten ontvangen kan.

Als u Hallo tekstbericht of telefoongesprek krijgt, code invoeren die u ontvangt in het tekstvak Hallo.

## <a name="credit-card-declined-or-not-accepted"></a>Creditcard is afgewezen, of wordt niet geaccepteerd
Virtueel of vooruitbetaalde creditcardgegevens kaarten zijn niet als betaling voor Azure-abonnementen geaccepteerd. Zie wat er kan ertoe leiden dat uw kaart toobe geweigerd, toosee [uw betaalpas of creditcard is afgewezen op Azure aanmelding](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>'Gratis proefversie is niet beschikbaar'
Hebt u een Azure-abonnement in de afgelopen Hallo gebruikt? Hello Azure gebruiksrechtovereenkomst beperkt gratis proefabonnement activering alleen voor een gebruiker die nieuwe tooAzure is. Als u een ander type Azure-abonnement hebt, kunt u een gratis proefversie niet activeren. U kunt zich aanmelden voor een [abonnement met betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Ik kosten met zich mee hebt gezien in Mijn account gratis proefversie
Mogelijk ziet u een klein controle houdt op uw creditcard-account nadat u zich aanmeldt, die binnen 3 too5 dagen wordt verwijderd. Als u bang over het beheer van kosten, lees meer over [voorkomen onverwachte kosten](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Dergelijke MSDN, BizSpark, BizSparkPlus of MPN Azure voordeel planning kan niet worden geactiveerd.
Zorg ervoor dat u rechts aanmelden Hallo referenties. Controleer vervolgens Hallo voordeel toomake ervoor dat u in aanmerking komende programma. 

* MSDN
  * Controleer of de status van de in aanmerking komt in uw [MSDN-accountpagina](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Als u de status van uw kan niet verifiëren, neem dan contact op met de Hallo [MSDN abonnementen Customer Service Centers](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Meld u aan toohello [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) en controleer of de status van de in aanmerking komt voor BizSpark en BizSpark Plus.
  * Als u de status kan niet controleren, kunt u [hulp krijgen op Hallo BizSpark forums](http://aka.ms/bzforums).
* MPN
  * Meld u aan toohello [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) en controleer of de status van de in aanmerking komt. Als u de juiste Hallo hebt [Cloud Platform vaardigheden](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), mogelijk in aanmerking komen voor extra voordelen.
  * Als u de status van uw kan niet verifiëren, neem dan contact op met [MPN ondersteuning](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Nieuw abonnement op Azure In Open activeren niet
een abonnement op Azure In Open toocreate, moet u een geldige sleutel van de Online Service-activering (OSA) met ten minste één Azure In Open-token gekoppeld tooit hebben. Als u een sleutel OSA geen hebt, neem contact op met een Microsoft-Partners die worden vermeld [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
