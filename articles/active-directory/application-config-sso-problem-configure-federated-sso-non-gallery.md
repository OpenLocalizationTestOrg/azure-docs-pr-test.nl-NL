---
title: configureren van federatieve eenmalige aanmelding voor een toepassing niet galerie aaaProblem | Microsoft Docs
description: Aantal Hallo veelvoorkomende problemen die optreden kunnen bij het configureren van federatieve eenmalige aanmelding tooyour aangepaste SAML-toepassing die niet wordt vermeld in de galerie van Azure AD-toepassing hello adres
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Probleem federatieve eenmalige aanmelding voor een toepassing niet galerie configureren

Als u een probleem ondervindt bij het configureren van een toepassing. Controleer of u alle stappen van Hallo in Hallo artikel hebt gevolgd [eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Een ander exemplaar van de toepassing hello toevoegen niet

tooadd een tweede exemplaar van een toepassing, moet u toobe kunnen:

-   Een unieke id voor de tweede instantie Hallo configureren. U kunt tooconfigure Hallo dezelfde id voor de eerste instantie Hallo gebruikt niet.

-   Configureer een ander certificaat dan Hallo gebruikt voor de eerste instantie Hallo.

Als hello toepassing biedt geen ondersteuning voor een van bovenstaande Hallo. Vervolgens niet kunnen tooconfigure een tweede exemplaar.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Waar kan ik Hallo id (gebruiker Identifier) van de entiteit indeling instellen

U kunt tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker niet.

Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling. Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder sectie Hallo NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Waar vind ik metagegevens van de toepassing hello of een certificaat van Azure AD

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
