---
title: federatiecertificaten aaaManage in Azure AD | Microsoft Docs
description: Meer informatie over hoe toocustomize Hallo vervaldatum voor uw federatiecertificaten en hoe toorenew certificaten die binnenkort verlopen.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Certificaten voor federatieve eenmalige aanmelding bij Azure Active Directory beheren
In dit artikel bevat informatie over veelgestelde vragen en informatie over de toohello certificaten dat tooestablish worden gemaakt met Azure Active Directory (Azure AD) voor federatieve eenmalige aanmelding (SSO) tooyour SaaS-toepassingen. Toepassingen van app-galerie van Azure AD Hallo of met behulp van een sjabloon voor niet-galerie toepassingen toevoegen Hallo toepassing configureren met behulp van Hallo federatieve SSO-optie.

Dit artikel is relevante alleen tooapps die geconfigureerd toouse Azure AD-eenmalige aanmelding via SAML-federation zijn, zoals wordt weergegeven in Hallo voorbeeld te volgen:

![Azure AD voor eenmalige aanmelding](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Automatisch gegenereerde certificaat voor de galerie en niet toepassingen
Wanneer u een nieuwe toepassing uit de galerie Hallo toevoegen en configureren van een SAML-gebaseerde aanmelding, genereert Azure AD een certificaat voor Hallo-toepassing die drie jaar geldig is. U kunt dit certificaat downloaden van Hallo **certificaat voor ondertekening van SAML** sectie. In deze sectie mogelijk voor galerie-toepassingen weer een optie toodownload Hallo certificaat of de metagegevens, afhankelijk van de vereiste Hallo van Hallo-toepassing.

![Azure AD eenmalige aanmelding](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Hallo-vervaldatum voor uw federation-certificaat aanpassen en overschakelen tooa nieuw certificaat
Standaard worden de certificaten tooexpire ingesteld na drie jaar. U kunt een andere vervaldatum voor het certificaat door Hallo volgende stappen uit te voeren.
Hallo schermafbeeldingen Salesforce gebruiken voor Hallo verjaardagen van voorbeeld, maar deze stappen tooany federatieve SaaS-app kunnen toepassen.

1. In Hallo [Azure-portal](https://aad.portal.azure.com), klikt u op **bedrijfstoepassing** in Hallo linker deelvenster en klik vervolgens op **nieuwe toepassing** op Hallo **overzicht** pagina:

   ![Open Hallo SSO-configuratiewizard](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Hallo galerie toepassing zoeken en selecteer vervolgens Hallo-toepassing die u tooadd wilt. Als u niet kunt toepassing hello vereist vinden, Hallo-toepassing toevoegen met behulp van Hallo **Non-galerie toepassing** optie. Deze functie is alleen beschikbaar in Hallo SKU van Azure AD Premium (P1 en P2).

    ![Azure AD eenmalige aanmelding](./media/active-directory-sso-certs/add_gallery_application.png)

3. Klik op Hallo **eenmalige aanmelding** koppeling in Hallo links deelvenster en wijzig **modus voor één aanmelding** te**op basis van SAML aanmelding**. Deze stap genereert een certificaat van de drie jaar voor uw toepassing.

4. een nieuw certificaat toocreate klikt u op Hallo **nieuw certificaat maken** koppeling in Hallo **certificaat voor ondertekening van SAML** sectie.

    ![Een nieuw certificaat genereren](./media/active-directory-sso-certs/create_new_certficate.png)

5. Hallo **Maak een nieuw certificaat** koppeling Hallo kalenderbesturingselement wordt geopend. U kunt instellen een datum en tijd van toothree jaar van Hallo huidige datum. Hallo geselecteerd datum en tijd is Hallo nieuwe datum en tijd van het nieuwe certificaat. Klik op **Opslaan**.

    ![Downloaden en vervolgens Hallo-certificaat uploaden](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Hallo nieuw certificaat is nu beschikbaar toodownload. Klik op Hallo **certificaat** koppeling toodownload deze. Uw certificaat is op dit moment niet actief. Als u wilt dat tooroll via toothis certificaat, selecteert u Hallo **nieuwe certificaat activeren** selectievakje in en klik op **opslaan**. Vanaf dat moment Azure AD wordt gestart met behulp van het nieuwe certificaat Hallo voor het Hallo-antwoord ondertekenen.

7.  toolearn het tooupload Hallo certificaat tooyour bepaalde SaaS-toepassing, klikt u op Hallo **weergave configuratie zelfstudie** koppeling.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Een certificaat vernieuwen dat binnenkort verloopt
Hallo moeten volgt vernieuwing resulteren in geen aanzienlijke uitvaltijd voor uw gebruikers. Hallo schermafbeeldingen in deze sectie functie Salesforce als een voorbeeld, maar deze stappen kunt tooany federatieve SaaS app toepassen.

1. Op Hallo **Azure Active Directory** toepassing **eenmalige aanmelding** pagina, nieuw certificaat voor uw toepassing hello genereren. U kunt dit doen door te klikken op Hallo **nieuw certificaat maken** koppeling in Hallo **certificaat voor ondertekening van SAML** sectie.

    ![Een nieuw certificaat genereren](./media/active-directory-sso-certs/create_new_certficate.png)

2. Selecteer Hallo gewenst datum en tijd voor uw nieuw certificaat en klik op **opslaan**.

3. Hallo-certificaat in Hallo downloaden **certificaat voor ondertekening van SAML** optie. Hallo nieuwe certificaat toohello SaaS-toepassing van configuratie voor één aanmelding scherm uploaden. toolearn hoe toodo voor uw bepaalde SaaS-toepassing, klikt u op Hallo **weergave configuratie zelfstudie** koppeling.
   
4. tooactivate hello nieuw certificaat in Azure AD, selecteer Hallo **nieuwe certificaat activeren** selectievakje en klikt u op Hallo **opslaan** knop bovenaan Hallo Hallo pagina. Hiermee wordt de via het nieuwe certificaat Hallo op Hallo Azure AD-zijde. Hallo-status van Hallo certificaat gewijzigd van **nieuw** te**Active**. Vanaf dat moment Azure AD wordt gestart met behulp van het nieuwe certificaat Hallo voor het Hallo-antwoord ondertekenen. 
   
    ![Een nieuw certificaat genereren](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Verwante artikelen:
* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Artikel index voor Toepassingsbeheer in Azure Active Directory](active-directory-apps-index.md)
* [Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Het oplossen van problemen op basis van SAML eenmalige aanmelding](active-directory-saml-debugging.md)
