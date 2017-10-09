---
title: cloudresources aaaSecure met Azure MFA en AD FS | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en AD FS in Hallo cloud.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Cloudresources beveiligen met Azure Multi-Factor Authentication en AD FS
Als uw organisatie is gefedereerd met Azure Active Directory, gebruikt u Azure multi-factor Authentication of Active Directory Federation Services (AD FS) toosecure resources die worden gebruikt door Azure AD. Hallo volgende procedures toosecure Azure Active Directory-resources met Azure multi-factor Authentication of Active Directory Federation Services gebruiken.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Azure AD-resources beveiligen met behulp van AD FS
toosecure uw cloudresource, instellen van een regel voor claims zodat Active Directory Federation Services Hallo multipleauthn claim verzendt wanneer een gebruiker wordt verificatie in twee stappen is uitgevoerd. Deze claim is tooAzure AD doorgegeven. Volg deze procedure toowalk Hallo stappen:


1. Open AD FS-beheer.
2. Selecteer aan de linkerkant Hallo **Relying Party-vertrouwensrelaties**.
3. Klik met de rechtermuisknop op **Identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Klik bij Uitgifte transformatieregels op**Regel toevoegen**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **doorgeven of filteren van een binnenkomende Claim** in Hallo vervolgkeuzelijst en klik op **volgende**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Geef de regel een naam. 
7. Selecteer **Verwijdingen verificatiemethode** als Hallo binnenkomende claimtype.
8. Selecteer **Alle claimwaarden doorgeven**.
    ![Wizard Claimregel voor transformatie toevoegen](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Klik op **Voltooien**. Sluit Hallo AD FS-beheerconsole.

## <a name="trusted-ips-for-federated-users"></a>Goedgekeurde IP-adressen voor federatieve gebruikers
Goedgekeurde IP-adressen kunnen beheerders de verificatie in twee stappen tooby pass voor specifieke IP-adressen of voor federatieve gebruikers met verzoeken die afkomstig zijn van hun eigen intranet. Hallo volgende secties wordt beschreven hoe tooconfigure Azure multi-factor Authentication goedgekeurde IP-adressen met federatieve gebruikers en de verificatie in twee stappen overslaan wanneer een aanvraag afkomstig van een federatieve gebruikers het intranet is. Dit wordt bereikt door het configureren van AD FS toouse doorgangsschijf of filteren van een binnenkomende claimsjabloon Hello claimtype binnen bedrijfsnetwerk.

In dit voorbeeld wordt Office 365 gebruikt voor onze Relying Party-vertrouwensrelaties.

### <a name="configure-hello-ad-fs-claims-rules"></a>Regels voor Hallo AD FS-claims configureren
Hallo eerst moet toodo is tooconfigure Hallo AD FS-claims. Twee claimregels maken, één voor Hallo binnen bedrijfsnetwerk claimtype en een extra regel om onze gebruikers aangemeld te houden.

1. Open AD FS-beheer.
2. Selecteer aan de linkerkant Hallo **Relying Party-vertrouwensrelaties**.
3. Klik met de rechtermuisknop op het **identiteitsplatform van Microsoft Office 365** en selecteer **Claimregels bewerken...**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Klik bij Uitgifte transformatieregels op**Regel toevoegen.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **doorgeven of filteren van een binnenkomende Claim** in Hallo vervolgkeuzelijst en klik op **volgende**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Hallo vak volgende tooClaim regelnaam de regel een naam geven. Bijvoorbeeld: BinnenBedrijfsNet.
7. Uit de vervolgkeuzelijst hello, volgende tooIncoming claimtype, selecteert **binnen bedrijfsnetwerk**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Klik op **Voltooien**.
9. Klik bij Uitgifte transformatieregels op**Regel toevoegen**.
10. Op Hallo transformeren Wizard Claimregel voor toevoegen, selecteert u **Claims verzenden met een aangepaste regel** in Hallo vervolgkeuzelijst en klik op **volgende**.
11. In het vak onder naam Claimregel Hallo: Voer *gebruikers aangemeld houden*.
12. Voer in het vak van het Hallo aangepaste regel:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Klik op **Voltooien**.
14. Klik op **Toepassen**.
15. Klik op **OK**.
16. Sluit AD FS-beheer.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Goedgekeurde IP-adressen van Azure Multi-Factor Authentication configureren bij federatieve gebruikers
Nu dat Hallo claims gemaakt zijn, kunnen we goedgekeurde IP-adressen configureren.

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Klik aan de linkerkant Hallo op **Active Directory**.
3. Selecteer onder adreslijst Hallo directory waar u tooset van goedgekeurde IP-adressen.
4. Op Hallo Directory die u hebt geselecteerd, klikt u op **configureren**.
5. Klik in de sectie multi-factor authentication hello, **service-instellingen beheren**.
6. Selecteer op Hallo pagina Service-instellingen onder goedgekeurde IP-adressen, **meerdere-multi-factor-verificatie overslaan voor aanvragen van federatieve gebruikers op mijn intranet**.  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Klik op **Opslaan**.
8. Zodra het Hallo-updates zijn toegepast, klikt u op **sluiten**.

Dat is alles. Federatieve gebruikers van Office 365 mag op dit moment alleen toouse MFA hebben wanneer een claim afkomstig van buiten Hallo bedrijfsintranet is.
