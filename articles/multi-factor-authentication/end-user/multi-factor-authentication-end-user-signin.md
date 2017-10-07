---
title: aaaAzure MFA aanmelden met verificatie in twee stappen | Microsoft Docs
description: Deze pagina vindt u u richtlijnen op waar toogo toosee Hallo verschillende aanmeldingsmethoden beschikbaar met Azure MFA.
keywords: verificatie van gebruikers, -aanmeldingservaring aanpast, aanmelden met een mobiele telefoon, aanmelden met een telefoon (werk)
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Hallo-aanmeldingservaring aanpast met Azure multi-factor Authentication
> [!NOTE]
> Hallo-doel van dit artikel is toowalk via een typische-aanmeldingservaring aanpast. Zie voor hulp bij het aanmelden of tootroubleshoot problemen, [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Wat is uw ervaring aanmelden?
Uw aanmeldingservaring is afhankelijk van wat u toouse als uw tweede factor kiest: een telefonische oproep of een app authentication teksten. Kies Hallo-optie die het beste beschrijft wat u doet:

| Hoe meld u aan? | 
| --- |
| [Met een telefonische oproep toomy mobile- of -telefoon](#signing-in-with-a-phone-call) |
| [Met een tekst toomy mobiele telefoon](#signing-in-with-a-text-message)
| [Met meldingen van Hallo Microsoft Authenticator-app](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Met verificatiecodes van Hallo Microsoft Authenticator-app](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Met een alternatieve methode omdat ik mijn voorkeursmethode nu kunt gebruiken](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Aanmelden met een telefonische oproep
Hallo volgende informatie beschrijft Hallo in twee stappen verificatie-ervaring met een aanroep tooyour mobiele telefoon of telefoon (werk).

1. Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.  
2. Microsoft roept u.  
3. Hallo telefoon te beantwoorden en druk op Hallo #-toets.  

## <a name="signing-in-with-a-text-message"></a>Aanmelden met een SMS-bericht
Hallo volgende informatie beschrijft Hallo in twee stappen verificatie-ervaring met een SMS-bericht tooyour mobiele telefoon:

1. Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord. 
2. Microsoft stuurt u een SMS-bericht met een aantal code. 
3. Hallo-code invoeren in Hallo daarvoor bestemde vak op de aanmeldingspagina Hallo. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Aanmelden met Hallo Microsoft Authenticator-app 
Hallo beschrijft volgende informatie de ervaring Hallo Hallo Microsoft Authenticator-app gebruiken voor verificatie in twee stappen. Er zijn twee verschillende manieren toouse Hallo-app. U kunt pushmeldingen kan ontvangen op uw apparaat kunt, of u Hallo app tooget een verificatiecode.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign met een melding van Hallo Microsoft Authenticator-app
1. Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.
2. Microsoft stuurt een melding toohello Microsoft Authenticator-app op uw apparaat.

  ![Microsoft verzendt melding](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Open Hallo melding op uw telefoon en selecteer Hallo **controleren** sleutel. Als uw bedrijf een PINCODE vereist is, moet u deze hier opgeven.
4. U moet nu worden aangemeld.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign aan met een verificatiecode met Hallo Microsoft Authenticator-app

Als u tooget verificatiecodes voor Hallo Microsoft Authenticator-app gebruikt, vervolgens ziet bij het openen van de app Hallo u een getal onder de accountnaam van uw. Deze waarde verandert elke 30 seconden, zodat u niet dezelfde tweemaal number Hallo gebruikt. Wanneer u wordt gevraagd een voor een verificatiecode Hallo app openen en gebruiken met het opgegeven getal momenteel wordt weergegeven. 

1. Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.
2. Microsoft vraagt u om een verificatiecode.

  ![Voer de verificatiecode in](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Open Hallo Microsoft Authenticator-app op uw telefoon en Hallo-code invoeren in Hallo vak waar u zich aanmeldt.

## <a name="signing-in-with-an-alternate-method"></a>Aanmelden met een alternatieve methode
Soms hebt u geen telefoon hello of een apparaat die u hebt ingesteld als uw contactmethode voorkeursoptie voor verificatie. Deze situatie is de reden waarom het is raadzaam dat u back-upmethoden voor uw account ingesteld. Hallo volgende sectie leest u hoe toosign aan met een alternatieve methode als uw primaire contactmethode mogelijk niet beschikbaar.

1. Meld u aan tooan toepassing of service zoals Office 365 met uw gebruikersnaam en wachtwoord.
2. Selecteer **gebruik een andere verificatieoptie**. Er zijn andere verificatie-opties op basis van hoeveel ingesteld hebt.
3. Selecteer een alternatieve methode en meld u aan.

  ![Alternatieve methode gebruiken](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Volgende stappen

Als u problemen met aanmelden met verificatie in twee stappen hebt, informatie op te krijgen [problemen hebt met Azure multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

Meer informatie over hoe te[de instellingen van de verificatie in twee stappen beheren](multi-factor-authentication-end-user-manage-settings.md).

Ontdek hoe u kunt te[aan de slag met Microsoft Authenticator-app Hallo](microsoft-authenticator-app-how-to.md) zodat u meldingen toosign in, in plaats van teksten en telefoongesprekken kunt. 
