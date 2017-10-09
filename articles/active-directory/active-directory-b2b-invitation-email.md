---
title: elementen van hello Azure Active Directory B2B-samenwerking uitnodigingsmail aaaThe | Microsoft Docs
description: Azure Active Directory B2B-samenwerking uitnodiging voor een e-mailsjabloon
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking

Een uitnodiging voor e-mailberichten zijn een essentieel onderdeel toobring partners boord B2B-samenwerking gebruikers in Azure AD. U kunt deze gebruiken tooincrease Hallo ontvanger vertrouwen. kunt u legitimiteit en sociale bewijs toohello e-mailadres toevoegen, toomake ervoor Hallo ontvanger werkt bekendheid met het selecteren van Hallo **aan de slag** knop tooaccept Hallo uitnodiging. Dit vertrouwen is dat een sleutel houdt tooreduce wrijving delen. En u wilt ook toomake Hallo e uiterlijk geweldig!

![Azure AD B2b-uitnodigingsmail](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Hallo-e-mailbericht waarin wordt uitgelegd
Bekijk enkele elementen Hallo e-mailadres zodat u hoe best toouse hun mogelijkheden weet.

### <a name="subject"></a>Onderwerp
Hallo onderwerp van e-mail Hallo volgt Hallo patroon volgen: U bent uitgenodigd toohello &lt;tenantname&gt; organisatie

### <a name="from-address"></a>Van-adres
We gebruiken een patroon LinkedIn-achtige voor Hallo van-adres.  U moet worden wie Hallo uitnodiging antwoorden is en waaruit de bedrijfsportal en ook verduidelijken dat e-Hallo afkomstig is van een e-mailadres van Microsoft. Hallo-indeling is: &lt;weergavenaam van de uitnodiging antwoorden&gt; van &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Beantwoorden
Hallo antwoord-tooemail toohello uitnodiging antwoorden van e-mail, indien beschikbaar, zodanig ingesteld dat toohello e-mail verzendt een e-mailbericht back toohello uitnodiging antwoorden beantwoorden.

### <a name="branding"></a>De huisstijl
Hallo uitnodiging voor een e-mailberichten van uw tenant gebruiken Hallo huisstijl die u hebt ingesteld voor uw tenant. Als u profiteren van deze mogelijkheid tootake wilt [hier](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) vindt u informatie over het Hallo tooconfigure deze. Hallo logo in banner wordt weergegeven in Hallo e-mailbericht. Ga als volgt Hallo afbeeldingsgrootte en kwaliteit instructies [hier](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) voor de beste resultaten. Bovendien Hallo bedrijfsnaam wordt ook weergegeven in Hallo aanroep tooaction.

### <a name="call-tooaction"></a>Aanroep tooaction
Hallo aanroep tooaction bestaat uit twee delen: waarin wordt uitgelegd waarom Hallo ontvanger Hallo mail heeft ontvangen en wat ontvanger hello wordt gevraagd toodo erover.
- Hallo "Waarom" sectie kan worden aangepakt met behulp van Hallo patroon volgen: U hebt uitgenodigde tooaccess toepassingen in Hallo zijn &lt;tenantname&gt; organisatie

- En de sectie 'wat u wordt gevraagd toodo' wordt aangegeven door de aanwezigheid van Hallo HALLO hallo **aan de slag** knop. Als Hallo ontvanger zonder Hallo uitnodigingen is toegevoegd, weergegeven deze knop niet.

### <a name="inviters-information"></a>De uitnodiging antwoorden informatie
Hallo uitnodiging antwoorden van weergavenaam is opgenomen in Hallo e-mail. En bovendien als u een profielfoto voor uw Azure AD-account hebt ingesteld, Hallo uitnodigen e omvatten ook afbeelding. Beide zijn beoogde tooincrease van de geadresseerde vertrouwen in Hallo e-mailbericht.

Als u nog uw profielfoto niet hebt ingesteld, wordt een pictogram met Hallo uitnodiging antwoorden van initialen in plaats van Hallo afbeelding wordt weergegeven:

  ![Hallo uitnodiging antwoorden van initialen weergeven](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Hoofdtekst
Hallo hoofdtekst bevat het Hallo-bericht dat Hallo uitnodiging antwoorden stelt het bericht of Hallo uitnodiging API is doorgegeven. Het is een tekstgebied, zodat deze geen HTML-tags uit veiligheidsoverwegingen verwerkt.

### <a name="footer-section"></a>Voettekstsectie
Hallo voettekst bevat Hallo Microsoft bedrijfsmerk en Hallo ontvanger weten als Hallo e-mailbericht is verzonden vanaf een niet-bewaakte alias kunt. Speciale gevallen:

- Hallo uitnodiging antwoorden geen een e-mailadres in Hallo tenancymodus uitgenodigd

  ![afbeelding van uitnodiging antwoorden geen een e-mailadres in Hallo tenancymodus uitgenodigd](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- Hallo ontvanger nodig tooredeem Hallo uitnodiging niet

  ![Wanneer de ontvanger tooredeem uitnodiging niet nodig](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B-samenwerking licentieverlening](active-directory-b2b-licensing.md)
* [Het oplossen van Azure Active Directory B2B-samenwerking](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B-samenwerking API en de aanpassing](active-directory-b2b-api.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
