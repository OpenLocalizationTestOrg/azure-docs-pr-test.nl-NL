---
title: aaaMicrosoft verificator phone aanmelden - Azure en Microsoft-accounts | Microsoft Docs
description: Gebruik uw telefoon toosign in tooyour Microsoft-account in plaats van uw wachtwoord te typen. Dit artikel worden veelgestelde vragen beantwoord over deze functie.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Meld u aan met uw telefoon niet uw wachtwoord

Hallo Microsoft Authenticator-app kunt u uw accounts beveiligen door verificatie in twee stappen uitvoert nadat u uw wachtwoord invoert. Maar wist u dat het Hallo-wachtwoord voor je persoonlijke Microsoft-account volledig kunt vervangen? 

Deze functie is beschikbaar op iOS en Android-apparaten en werkt met persoonlijke Microsoft-accounts. 

## <a name="how-it-works"></a>Hoe werkt het?

Veel van u Hallo Microsoft Authenticator-app gebruiken voor verificatie in twee stappen wanneer u zich aanmeldt tooyour Microsoft-account. U Typ uw wachtwoord en ga vervolgens toohello app tooeither een melding goedkeuren of maak een verificatiecode. Met phone aanmelden, Hallo wachtwoord overslaan en alle ID-verificatie uitvoeren op uw telefoon. Omdat het is een soort verificatie in twee stappen phone aanmelden, moet u nog steeds tooprovide een ding dat u weet en een ding dat u uw identiteit tooverify hebt. Hallo phone nog steeds Hallo wat die u hebt en de PINCODE of biometrische sleutel van uw telefoon is Hallo wat die u weet. 

## <a name="how-tooget-started"></a>Hoe tooget gestart

toosign in tooyour persoonlijke Microsoft-account met uw telefoon als volgt te werk: 

1. Telefoon-aanmeldingspagina voor uw account inschakelen. 

  - Als er geen Hallo Microsoft Authenticator-app nog, installeren en toevoegen van uw persoonlijke Microsoft-account op basis van toohello stappen op Hallo [Microsoft Authenticator pagina](microsoft-authenticator-app-how-to.md). Toegevoegde accounts worden automatisch ingeschakeld, zodat u goed toogo.

  - Als u Microsoft Authenticator al voor verificatie in twee stappen gebruikt, selecteert u uw account op de introductiepagina Hallo-app en selecteer **inschakelen aanmeldingspagina phone** uit de vervolgkeuzelijst Hallo.

  >[!NOTE] 
  >tooprotect uw account moet een PINCODE of biometrische vergrendeling op uw apparaat. Als u uw telefoon ontgrendeld, verschijnt Hallo-app wordt een aanvraag waarin u wordt gevraagd tooset van een vergrendeling voordat u de aanmeldingspagina phone inschakelt. 

3. De meeste pagina's waar normaal u het wachtwoord voor je Microsoft-account voert hebben een koppeling met de tekst **gebruik van een app in plaats daarvan**. Selecteer deze koppeling toosign aan met uw telefoon. 

4. Microsoft verzendt een melding tooyour telefoon. Hallo melding toosign in tooyour-account goedkeuren.   

## <a name="faq"></a>Veelgestelde vragen 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>Hoe wordt aanmelden met mijn telefoon veiliger dan een wachtwoord te typen?  

Vandaag de meeste mensen aanmelden tooweb sites of toepassingen met een gebruikersnaam en wachtwoord.  Helaas zijn wachtwoorden vaak verloren, gestolen of geraden door hackers. Wanneer u Hallo Microsoft Authenticator-app toosign in instelt, moet er een sleutel op uw telefoon die u kunt uw account ontgrendelen gegenereerd. Beveiligen we deze sleutel Hello PINCODE of biometrische dat u al op uw telefoon gebruiken.  Wanneer u zich met uw telefoon aanmeldt, deze sleutel is gebruikte tooprove je identiteit veilig met twee – hello factoren phone zelf en de mogelijkheid toounlock deze. 

Hallo-sleutel die wordt gebruikt, is vergelijkbaar toohello sleutels die worden gebruikt in Windows Hello en Hallo FIDO Alliance UAF specificaties. Uw gegevens alleen is biografie wordt gebruikt tooprotect Hallo sleutel lokaal, en nooit verzonden naar of opgeslagen in de cloud Hallo. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>Waar kan ik mijn telefoon tooreplace gebruiken mijn wachtwoord en waar moet ik de nog steeds Hallo wachtwoord?  

Vandaag de dag Hallo phone aanmelden functie wordt alleen werkt met web-apps en services die door de persoonlijke Microsoft-accounts, iOS of Android-apps die gebruikmaken van een persoonlijk Microsoft-account en op Windows 10-apps die gebruikmaken van een persoonlijk Microsoft-account is ingeschakeld. Wanneer u zich aanmeldt tooone van deze websites of toepassingen, op Hallo pagina waar u meestal Voer uw wachtwoord wordt een koppeling met de tekst **gebruik van een app in plaats daarvan**. 

Telefoon mag teken-niet gebruikte toounlock een Windows-PC, XBOX of bureaublad versies van Microsoft-apps, zoals Office-apps op dit moment. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Vervangt deze verificatie in twee stappen? Moet ik uitschakelen?   

Soms. We proberen uit te breiden Hallo-bereik van de aanmeldingspagina telefoon, maar nu er nog steeds plaatsen in de Microsoft-ecosysteem Hallo die niet ondersteund. In deze locaties we verificatie in twee stappen nog steeds gebruiken voor veilige aanmelden. Daarom moet Nee, niet moet u uitschakelen verificatie in twee stappen voor uw account. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>Goed, als ik verificatie in twee stappen ingeschakeld voor mijn account houden, heb ik tooapprove twee meldingen?

U niet Nee, het volgende geval. Microsoft-account met uw telefoon tooyour aanmelden telt als verificatie in twee stappen. In plaats van te typen in het wachtwoord, en vervolgens een melding goedkeuren u uw identiteit bewijzen door weten hoe toounlock uw telefoon en vervolgens een melding goedkeuren. We won't sturen u een tweede melding tooapprove.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>Wat gebeurt er als ik mijn telefoon verlies of met me niet hebt, hoe kan ik toegang tot mijn account?  

U kunt altijd klikken op **gebruik in plaats daarvan een wachtwoord** op Hallo aanmeldingspagina tooswitch back toousing uw wachtwoord. Houd er rekening mee dat als u verificatie in twee stappen hebt gebruikt, u toch een tweede methode tooverify bent aangemeld moet. Daarom is we raden je toomake ervoor dat er extra, up-to-date beveiligingsgegevens voor je account. U kunt de beveiligingsgegevens voor je op https://account.live.com/proofs/manage beheren. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Hoe stoppen met het gebruik van deze functie en ik ga terug tooentering mijn wachtwoord?

Klik op **gebruik in plaats daarvan een wachtwoord** wanneer u zich aanmeldt. We de meest recente keuze onthouden en bieden die door een standaard Hallo wanneer die u zich aanmeldt. Als u ooit toogo back toosigning aan met uw telefoon wilt, klikt u op **gebruik van een app in plaats daarvan**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>Kan ik gebruiken Hallo app toosign in tooall mijn accounts met Microsoft?   
Deze functionaliteit is alleen beschikbaar voor persoonlijke Microsoft-accounts op dit moment. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Kan ik aanmelden bij deze PC met mijn telefoon?  
Voor uw PC aangeraden aanmelden met Windows Hello op Windows 10 met uw face vingerafdruk of een PINCODE.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>Kan ik Meld u aan met mijn Windows Phone?  
Op dit moment ontwikkelt we deze functionaliteit voor Hallo Microsoft Authenticator op Windows Phone niet. 

## <a name="next-steps"></a>Volgende stappen
Als u dit nog niet hebt gedownload Hallo Microsoft Authenticator-app, het uitchecken. Hallo-app is beschikbaar voor [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), en is beschikbaar op Hallo Microsoft Authenticator-app voor aanmeldingspagina phone [Android](http://go.microsoft.com/fwlink/?Linkid=825072) en [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Als u vragen over Hallo-app in het algemeen hebt, bekijk Hallo [verificator Veelgestelde vragen over Microsoft](microsoft-authenticator-app-faq.md)
