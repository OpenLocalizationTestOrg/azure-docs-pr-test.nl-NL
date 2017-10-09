---
title: aaaError op de pagina van de toepassing na het aanmelden | Microsoft Docs
description: Hoe tooresolve problemen met Azure AD aanmelden bij het Hallo-toepassing zelf genereert een fout opgetreden
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Fout op de pagina voor een toepassing na het aanmelden

In dit scenario Azure AD Hallo-gebruiker in heeft ondertekend, maar Hallo toepassing is een fout opgetreden bij het Hallo gebruiker toosuccessfully voltooien Hallo teken is niet toegestaan in stroom om weer te geven. In dit scenario accepteert Hallo toepassing geen Hallo antwoord probleem door Azure AD.

Er zijn enkele mogelijke redenen waarom Hallo toepassing hello Azure AD-antwoord niet geaccepteerd. Als het Hallo-fout in de toepassing hello is niet genoeg wissen tooknow ontbreekt wat Hallo antwoord wordt vervolgens:

-   Controleer of u alle stappen van Hallo in Hallo artikel hebt uitgevoerd als Hallo toepassing hello Azure AD-galerie, [hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Gebruik een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) toocapture SAML SAML-reactie en SAML-token aanvragen.

-   Hallo SAML-reactie delen met Hallo toepassing leverancier tooknow wat ontbreekt.

## <a name="missing-attributes-in-hello-saml-response"></a>Ontbrekende kenmerken in Hallo SAML-reactie

een kenmerk in hello Azure AD configuratie toobe verzonden in antwoord hello Azure AD, tooadd Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op **weergeven en alle andere gebruiker onder kenmerken bewerken** hello **gebruikerskenmerken** sectie tooedit Hallo kenmerken toobe verzonden toohello toepassing in Hallo SAML-token wanneer de gebruiker zich aanmelden.

   een kenmerk tooadd:

   * Klik op **toevoegen kenmerk**. Voer Hallo **naam** en selecteer Hallo Hallo **waarde** uit Hallo vervolgkeuzelijst.

   * Klik op **opslaan.** U zien nieuw kenmerk Hallo in Hallo tabel.

9.  Hallo-configuratie op te slaan.

Volgende keer Hallo gebruiker zich aanmeldt toohello toepassing, Azure AD verzenden Hallo nieuw kenmerk in Hallo SAML-reactie.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>Hallo-toepassing verwacht een andere gebruikers-id-waarde of de indeling

Hallo is aanmelden toohello toepassing mislukt omdat Hallo SAML-reactie kenmerken, zoals rollen ontbreekt of omdat het Hallo-toepassing een andere indeling voor het Hallo-id van de entiteit-kenmerk worden verwacht.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Een kenmerk in de configuratie van hello Azure AD-toepassing toevoegen:

toochange hello gebruikers-id-waarde Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Onder Hallo **gebruikerskenmerken**, selecteer de unieke id voor uw gebruikers in Hallo Hallo **gebruikers-id** vervolgkeuzelijst.

## <a name="change-entityid-user-identifier-format"></a>Wijzigen van de id van de entiteit (gebruikers-id)

Als de toepassing hello een andere indeling voor het Hallo-id van de entiteit-kenmerk verwacht. Vervolgens niet kunnen tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker.

Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling. Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder Hallo sectie NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>Hallo-toepassing verwacht een andere handtekening-methode voor het SAML-reactie Hallo

toochange welke onderdelen van het SAML-token Hallo digitaal zijn ondertekend door Azure Active Directory. Volg onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder Hallo **certificaat voor ondertekening van SAML** sectie.

9.  Selecteer Hallo juiste **ondertekening optie** werd verwacht door de toepassing hello:

  * Meld u SAML-reactie

  * Meld u aan de SAML-reactie en verklaring

  * Aanmelding van SAML-verklaring

Volgende keer Hallo gebruiker zich aanmeldt toohello toepassing, Hallo Azure AD-aanmelding deel uit van SAML-reactie Hallo geselecteerd.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>Hallo-toepassing verwacht hello toobe algoritme SHA-1-ondertekening

Standaard ondertekent Azure AD Hallo SAML-token met Hallo meeste beveiliging wordt gebruikt. Niet Hallo-algoritme tooSHA-1 is raadzaam wijzigen tenzij Hallo toepassing vereist.

toochange Hallo ondertekeningsalgoritme, volgt u onderstaande Hallo stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op **weergeven geavanceerde instellingen voor het ondertekenen van certificaat** onder Hallo **certificaat voor ondertekening van SAML** sectie.

9.  Selecteer SHA-1 in Hallo **ondertekening algoritme**.

Volgende keer dat de gebruiker zich aanmeldt toohello toepassing hello, Azure AD-aanmelding Hallo SAML-token met behulp van algoritme SHA-1.

## <a name="next-steps"></a>Volgende stappen
[Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
