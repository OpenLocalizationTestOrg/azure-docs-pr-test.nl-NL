---
title: aaaProblems aanmelden tooa galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding | Microsoft Docs
description: Richtlijnen voor het Hallo specifieke fouten bij het ondertekenen van een toepassing die u hebt geconfigureerd voor op basis van SAML federatieve eenmalige aanmelding met Azure AD
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>Problemen met aanmelden tooa galerie toepassing is geconfigureerd voor federatieve eenmalige aanmelding

tootroubleshoot uw probleem, moet u tooverify Hallo Toepassingsconfiguratie in Azure AD als volgt:

-   U kunt alle Hallo configuratiestappen voor Azure AD-galerie toepassing hello hebt gevolgd.

-   Hallo-id en de antwoord-URL is geconfigureerd in AAD overeenkomen ze verwachte waarden in de toepassing hello

-   U hebt toegewezen gebruikers toohello toepassing

## <a name="application-not-found-in-directory"></a>Toepassing is niet gevonden in map

*Fout AADSTS70001: Toepassing met id 'https://contoso.com' is niet gevonden in de directory Hallo*.

**Mogelijke oorzaak**

Hallo verlener kenmerk verzendt van Hallo toepassing tooAzure AD in Hallo SAML-aanvraag komt niet overeen met de id-waarde Hallo geconfigureerd in de toepassing hello Azure AD.

**Naamomzetting**

Zorg ervoor dat kenmerk Hallo verlener in Hallo SAML-aanvraag dat deze komt overeen met de Hallo id waarde die is geconfigureerd in Azure AD:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**domein en de URL's** sectie. Controleer of u die waarde Hallo in Hallo id textbox is die overeenkomt met Hallo-waarde voor Hallo id-waarde weergegeven in het Hallo-fout.

Nadat u de id-waarde Hallo hebt bijgewerkt in Azure AD en de overeenkomende Hallo waarde door de toepassing hello in Hallo SAML-aanvraag verzendt, moet u kunnen toosign in toohello toepassing.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>Hallo antwoordadres komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello.

*Fout AADSTS50011: antwoordadres Hallo 'https://contoso.com' komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello*

**Mogelijke oorzaak**

Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag komt niet overeen met de Hallo antwoord-URL-waarde of patroon dat is geconfigureerd in Azure AD. Hallo AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag is Hallo-URL die u in Hallo-fout ziet.

**Naamomzetting**

Zorg ervoor dat Hallo AssertionConsumerServiceURL de waarde in Hallo SAML-aanvraag de overeenkomende Hallo antwoord-URL-waarde die is geconfigureerd in Azure AD.

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**domein en de URL's** sectie. Controleren of bijwerken van Hallo-waarde in Hallo antwoord-URL textbox toomatch hello AssertionConsumerServiceURL waarde in Hallo SAML-aanvraag.  
    * Als u Hallo antwoord-URL textbox niet ziet, selecteert u Hallo **weergeven geavanceerde instellingen voor URL** selectievakje.

Nadat u Hallo antwoord-URL-waarde hebben bijgewerkt in Azure AD en het Hallo-waarde die overeenkomt met verzendt door toepassing hello in Hallo SAML-aanvraag, moet u kunnen toosign in toohello toepassing.

## <a name="user-not-assigned-a-role"></a>Gebruiker met een niet toegewezen

*Fout AADSTS50105: Hallo aangemelde gebruiker 'brian@contoso.com' is niet toegewezen rol voor de toepassing hello tooa*.

**Mogelijke oorzaak**

Hallo-gebruiker is niet verleend access toohello-toepassing in Azure AD.

**Naamomzetting**

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.

Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.

## <a name="not-a-valid-saml-request"></a>Geen een geldige SAML aanvragen

*Fout AADSTS75005: Hallo-aanvraag is niet een geldig Saml2-protocolbericht.*

**Mogelijke oorzaak**

Hallo SAML-aanvraag verzonden door de toepassing hello voor eenmalige aanmelding biedt geen ondersteuning voor Azure AD. Enkele veelvoorkomende problemen zijn:

-   Ontbrekende vereiste velden in Hallo SAML-aanvraag

-   SAML gecodeerd aanvraagmethode

**Naamomzetting**

1.  Vastleggen van SAML-aanvraag. Volg de zelfstudie Hallo [hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn hoe toocapture Hallo SAML aanvragen.

2.  Neem contact op met de leverancier van de toepassing hello en -share:

   -   SAML-aanvraag

   -   [Vereisten voor Azure AD Single Sign-on SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Ze moeten valideren hello Azure AD SAML-implementatie voor eenmalige aanmelding ondersteund.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Er is geen resource in de lijst requiredResourceAccess

*Fout AADSTS65005:hello clienttoepassing toegang tooresource heeft aangevraagd ' 00000002-0000-0000-c000-000000000000'. Deze aanvraag is mislukt omdat het Hallo-client is niet opgegeven voor deze bron in de lijst met requiredResourceAccess*.

**Mogelijke oorzaak**

Hallo application-object is beschadigd.

**Oplossing: optie 1**

toosolve hello probleem Hallo unieke id-waarde in hello Azure AD-configuratie toevoegen. een id-waarde tooadd Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu

8.  Onder Hallo **domein en de URL** sectie, moet u controleren op Hallo **weergeven geavanceerde instellingen voor URL**.

9.  in Hallo **id** textbox Typ een unieke id voor de toepassing hello.

10. **Sla** Hallo-configuratie.


**Optie 2 voor naamomzetting**

Als optie 1 hierboven niet werkt, probeert u het Hallo-toepassing worden verwijderd uit Hallo directory. Vervolgens toevoegen en configureren van de toepassing hello, volg onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Klik op **verwijderen** op Hallo linksboven van de toepassing hello **overzicht** blade.

8.  Vernieuwen van Azure AD en voegt u de toepassing hello van Hallo-galerie van Azure AD. Configureer vervolgens de toepassing hello

<span id="_Hlk477190176" class="anchor"></span>Na het opnieuw configureren van de toepassing hello, moet u kunnen toosign in toohello toepassing.

## <a name="certificate-or-key-not-configured"></a>Certificaat of de sleutel niet geconfigureerd

*Fout AADSTS50003: Er is geen ondertekeningssleutel geconfigureerd.*

**Mogelijke oorzaak**

Hallo application-object is beschadigd en Azure AD geconfigureerd voor de toepassing hello Hallo-certificaat niet wordt herkend.

**Naamomzetting**

toodelete en maak een nieuw certificaat, volgt u onderstaande Hallo stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

 * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op **nieuw certificaat maken** onder Hallo **SAML handtekeningcertificaat** sectie.

9.  Selecteer de vervaldatum. Klik vervolgens op **opslaan.**

10. Controleer **nieuwe certificaat activeren** toooverride Hallo actieve certificaat. Klik vervolgens op **opslaan** Hallo boven aan het Hallo-blade tooactivate Hallo rollovercertificaat en accepteren.

11. Onder Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **verwijderen** tooremove hello **ongebruikt** certificaat.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Probleem bij het aanpassen van Hallo SAML claims verzonden tooan toepassing

toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
[Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
