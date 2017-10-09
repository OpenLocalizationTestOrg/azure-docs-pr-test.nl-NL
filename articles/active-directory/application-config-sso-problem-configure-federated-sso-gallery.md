---
title: aaaProblem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren | Microsoft Docs
description: Adres aantal Hallo veelvoorkomende problemen optreden kunnen bij het configureren van federatieve eenmalige aanmelding via SAML voor toepassingen die worden vermeld in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Probleem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren

Als u een probleem ondervindt bij het configureren van een toepassing. Controleer of dat u alle Hallo stappen hebt gevolgd in de zelfstudie Hallo voor Hallo-toepassing. In de configuratie van de toepassing hello hebt u inline-documentatie over hoe tooconfigure toepassing hello. U kunt ook openen Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.

## <a name="cant-add-another-instance-of-hello-application"></a>Een ander exemplaar van de toepassing hello toevoegen niet

tooadd een tweede exemplaar van een toepassing, moet u toobe kunnen:

-   Een unieke id voor de tweede instantie Hallo configureren. U kunt tooconfigure Hallo dezelfde id voor de eerste instantie Hallo gebruikt niet.

-   Configureer een ander certificaat dan Hallo gebruikt voor de eerste instantie Hallo.

Als hello toepassing biedt geen ondersteuning voor een van bovenstaande Hallo. Vervolgens niet kunnen tooconfigure een tweede exemplaar.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Kan geen Hallo id toevoegen of Hallo antwoord-URL

Als u niet kunt tooconfigure Hallo id of Hallo antwoord-URL, Hallo id bevestigen en antwoord-URL waarden Hallo patronen vooraf is geconfigureerd voor de toepassing hello overeenkomen.

tooknow hello patronen vooraf is geconfigureerd voor de toepassing hello:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.** Ga toostep 7. Als u al Hallo toepassing configuratie blade op Azure AD.

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.

9.  Ga toohello **id** of **antwoord-URL** textbox onder Hallo **sectie domein en URL's.**

10. Er zijn drie manieren tooknow Hallo ondersteund patronen voor Hallo toepassing:

   * Hallo textbox u ziet Hallo ondersteund patroon of patronen als tijdelijke aanduiding *voorbeeld:* <https://contoso.com>.

   * Als het Hallo-patroon wordt niet ondersteund, ziet u een rood uitroepteken wanneer u tooenter Hallo waarde in Hallo textbox probeert. Als u de muisaanwijzer op Hallo rood uitroepteken, ziet u Hallo ondersteund patronen.

   * In de zelfstudie Hallo voor toepassing hello, kunt u ook informatie ophalen over Hallo ondersteund patronen. Onder Hallo **eenmalige aanmelding configureren Azure AD** sectie. Ga toohello stap voor het geconfigureerde Hallo waarden onder Hallo **domein en de URL's** sectie.

Als de waarden Hallo komen niet met Hallo patronen vooraf is geconfigureerd op Azure AD overeen. U kunt:

-   Werken met Hallo toepassing leverancier tooget waarden die overeenkomen met Hallo patroon vooraf is geconfigureerd op Azure AD

-   U kunt ook contact opnemen met Azure AD-team via < aadapprequest@microsoft.com > of u een reactie in Hallo zelfstudie toorequest Hallo bijwerken van de patronen voor Hallo toepassing hello ondersteund

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Waar kan ik Hallo id (gebruiker Identifier) van de entiteit indeling instellen

U kunt tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker niet.

Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling. Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder sectie Hallo NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Kan hello Azure AD metagegevens toocomplete Hallo configuratie met Hallo toepassing niet vinden

de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom. Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.

Azure AD biedt een URL tooget Hallo metagegevens niet. Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Niet weet hoe toocustomize SAML claims tooan toepassing verzonden

toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)
