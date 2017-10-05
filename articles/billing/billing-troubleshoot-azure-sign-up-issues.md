---
title: Oplossen van problemen met Azure aanmelding | Microsoft Docs
description: Hierin wordt beschreven hoe u een aantal algemene Azure aanmelding oplossen problemen omhoog.
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
ms.openlocfilehash: 647509ea36e487aca5db661adb3268e845988f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Problemen oplossen van problemen met aanmelding voor Azure
Gebruik de tips in dit artikel als u niet kunt voor Azure aanmelden, veelvoorkomende problemen kunt oplossen. Als er een probleem met je creditcard tijdens het aanmelden, Zie [uw betaalpas of creditcard is afgewezen op Azure aanmelding](billing-credit-card-fails-during-azure-sign-up.md). Als u Azure-account hebt, maar u kunt zich niet aanmelden, Zie [ik kan niet aanmelden bij het beheren van mijn Azure-abonnement](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>De voortgangsbalk reageert niet meer in de sectie 'Identiteitscontrole door kaart'

De om identiteitverificatie te voltooien door kaart, moeten cookies van derden worden toegestaan voor uw browser.

![Schermafbeelding van de verificatie door de sectie van de kaart is verkeerd-om tijdens de registratie van de identiteit](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Gebruik de volgende stappen voor het bijwerken van uw browser cookie-instellingen.

1. Als u Chrome, gaat u naar **instellingen** > **weergeven geavanceerde instellingen** > **Privacy** > **instellingen**. Schakel het selectievakje **blokkeren van cookies van derden en sitegegevens**.
2. Als u Edge gebruikt, gaat u naar **instellingen** > **weergave geavanceerde instellingen** > **Cookies**. Selecteer **geen cookies blokkeren**.
3. Vernieuw de registratiepagina in Azure en controleer of het probleem opgelost is.
4. Als het probleem niet kunt met het vernieuwen oplossen, sluit af en start de browser opnieuw en probeer het opnieuw.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Creditcardformulier biedt geen ondersteuning voor Mijn factuuradres
Je factuuradres moet zich in het land dat u hebt geselecteerd in de **over u** sectie. Zorg ervoor dat u het juiste land selecteren.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Er is geen SMS-berichten of aanroepen tijdens de registratie accountverificatie
Het is meestal veel sneller, duurt maximaal vier minuten verificatiecode in die moet worden geleverd. Het telefoonnummer op dat u voor de verificatie invoert is niet opgeslagen als een telefoonnummer voor het account.

Hier volgen enkele aanvullende tips:
* Een VOIP-telefoonnummer kan niet worden gebruikt voor de verificatieprocedure.
* Controleer het telefoonnummer dat u invoert, inclusief de landcode die u hebt geselecteerd in de vervolgkeuzelijst.
* Als uw telefoon geen tekstberichten (SMS) ontvangt, probeert de **Bel me** optie.
* Zorg ervoor dat uw telefoon aanroepen of SMS-berichten van een getal van de Verenigde Staten ontvangen kan.

Als u de tekstbericht of telefoongesprek krijgt, code invoeren die u ontvangt in het tekstvak.

## <a name="credit-card-declined-or-not-accepted"></a>Creditcard is afgewezen, of wordt niet geaccepteerd
Virtueel of vooruitbetaalde creditcardgegevens kaarten zijn niet als betaling voor Azure-abonnementen geaccepteerd. Zie Wat kan leiden tot de kaart wordt geweigerd [uw betaalpas of creditcard is afgewezen op Azure aanmelding](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>'Gratis proefversie is niet beschikbaar'
Hebt u een Azure-abonnement in het verleden gebruikt? De gebruiksvoorwaarden voor Azure-overeenkomst beperkt gratis proefabonnement activering alleen voor een gebruiker die is nieuw in Azure. Als u een ander type Azure-abonnement hebt, kunt u een gratis proefversie niet activeren. U kunt zich aanmelden voor een [abonnement met betalen naar gebruik](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Ik kosten met zich mee hebt gezien in Mijn account gratis proefversie
Mogelijk ziet u een klein controle houdt op uw creditcard-account nadat u zich aanmeldt, die binnen 3 tot 5 dagen wordt verwijderd. Als u bang over het beheer van kosten, lees meer over [voorkomen onverwachte kosten](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Dergelijke MSDN, BizSpark, BizSparkPlus of MPN Azure voordeel planning kan niet worden geactiveerd.
Zorg ervoor dat u de juiste referenties. Controleer het voordeel programma om ervoor te zorgen dat je in aanmerking komt. 

* MSDN
  * Controleer of de status van de in aanmerking komt in uw [MSDN-accountpagina](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Als u de status van uw kan niet verifiëren, neem dan contact op met de [MSDN abonnementen Customer Service Centers](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Aanmelden bij de [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) en controleer of de status van de in aanmerking komt voor BizSpark en BizSpark Plus.
  * Als u de status kan niet controleren, kunt u [hulp krijgen op de forums BizSpark](http://aka.ms/bzforums).
* MPN
  * Aanmelden bij de [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) en controleer of de status van de in aanmerking komt. Als u beschikt over de juiste [Cloud Platform vaardigheden](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), mogelijk in aanmerking komen voor extra voordelen.
  * Als u de status van uw kan niet verifiëren, neem dan contact op met [MPN ondersteuning](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Nieuw abonnement op Azure In Open activeren niet
U moet een geldige sleutel van de Online Service-activering (OSA) met ten minste één Azure In Open-token die is gekoppeld aan deze hebben voor het maken van een Azure In Open-abonnement. Als u een sleutel OSA geen hebt, neem contact op met een Microsoft-Partners die worden vermeld [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.
