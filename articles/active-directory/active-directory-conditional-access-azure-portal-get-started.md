---
title: aaaGet de slag met voorwaardelijke toegang in Azure Active Directory | Microsoft Docs
description: Voorwaardelijke toegang met behulp van een locatie voorwaarde testen.
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>Aan de slag met voorwaardelijke toegang in Azure Active Directory

Voorwaardelijke toegang is een functie van Azure Active Directory waarmee u toodefine voorwaarden waaronder gemachtigde gebruikers toegang uw apps tot hebben. 

In dit onderwerp vindt u instructies voor het testen van een voorwaardelijke toegang op basis van de voorwaarde van een locatie in uw omgeving.  


## <a name="scenario-description"></a>Scenariobeschrijving

Een van de algemene vereisten in veel organisaties is tooonly meervoudige verificatie vereisen voor toegang tooapps die niet van het bedrijfsintranet hello wordt uitgevoerd. Met Azure Active Directory, kunt u eenvoudig deze doelstelling uitvoeren door het configureren van beleid voor voorwaardelijke toegang op basis van locatie. Dit onderwerp vindt u gedetailleerde instructies voor het configureren van een gerelateerd beleid. maakt gebruik van beleid Hallo [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish tussen toegangspogingen tot van zakelijke Hallo de intranet- en alle andere locaties.


## <a name="prerequisites"></a>Vereisten

Hallo scenario beschreven in dit onderwerp wordt ervan uitgegaan dat u bekend met Hallo concepten die worden beschreven bent in [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).

tootest dit scenario moet u:

- Een testgebruiker maken 

- Wijs een licentie voor Azure AD Premium toohello testgebruiker

- Configureren van een beheerde app en uw test gebruiker tooit toewijzen

- Goedgekeurde IP-adressen configureren

Als u meer informatie over de goedgekeurde IP-adressen, Zie [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="policy-configuration-steps"></a>Beleid configuratiestappen

**tooconfigure uw beleid voor voorwaardelijke toegang, doen:**

1. Klik in hello Azure-portal op Hallo links navigatiebalk, op **Azure Active Directory**. 

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. Op Hallo **Azure Active Directory** blade in Hallo **beheren** sectie, klikt u op **voorwaardelijke toegang**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. Op Hallo **voorwaardelijke toegang** blade, tooopen hello **nieuw** blade in de werkbalk Hallo op Hallo boven, klikt u op **toevoegen**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. Op Hallo **nieuw** blade in Hallo **naam** textbox, typ een naam voor uw beleid.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. In Hallo **toewijzing** sectie, klikt u op **gebruikers en groepen**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. Op Hallo **gebruikers en groepen** blade Hallo volgende stappen uit te voeren:

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. Klik op **gebruikers en groepen selecteren**.

    b. Klik op **Selecteren**.

    c. Op Hallo **Selecteer** blade uw testgebruiker selecteren en klik vervolgens op **Selecteer**.

    d. Op Hallo **gebruikers en groepen** blade, klikt u op **gedaan**.

7. Op Hallo **nieuw** blade, tooopen hello **Cloud-apps** blade in Hallo **toewijzing** sectie, klikt u op **Cloud-apps**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. Op Hallo **Cloud-apps** blade Hallo volgende stappen uit te voeren:

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. Klik op **apps selecteren**.

    b. Klik op **Selecteren**.

    c. Op Hallo **Selecteer** blade uw cloud-app selecteren en klik vervolgens op **Selecteer**.

    d. Op Hallo **Cloud-apps** blade, klikt u op **gedaan**.

9. Op Hallo **nieuw** blade, tooopen hello **voorwaarden** blade in Hallo **toewijzing** sectie, klikt u op **voorwaarden**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. Op Hallo **voorwaarden** blade, tooopen hello **locaties** blade, klikt u op **locaties**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. Op Hallo **locaties** blade Hallo volgende stappen uit te voeren:

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. Onder **configureren**, klikt u op **Ja**.

    b. Onder **opnemen**, klikt u op **alle locaties**.

    c. Klik op **uitsluiten**, en klik vervolgens op **alle goedgekeurde IP-adressen**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. Klik op **Gereed**.

12. Op Hallo **voorwaarden** blade, klikt u op **gedaan**.

13. Op Hallo **nieuw** blade, tooopen hello **Grant** blade in Hallo **besturingselementen** sectie, klikt u op **Grant**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. Op Hallo **Grant** blade Hallo volgende stappen uit te voeren:

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. Selecteer **meervoudige authenticatie**.

    b. Klik op **Selecteren**.

15. Op Hallo **nieuw** blade onder **beleid inschakelen**, klikt u op **op**.

    ![Voorwaardelijke toegang](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. Op Hallo **nieuw** blade, klikt u op **maken**.


## <a name="testing-hello-policy"></a>Hallo beleid testen

tootest uw beleid, moet u toegang tot uw app vanaf een apparaat dat: 

1. Heeft een IP-adres dat binnen de geconfigureerde goedgekeurde IP-adressen 

1. Heeft een IP-adres dat is niet binnen de geconfigureerde goedgekeurde IP-adressen

Multi-factor authentication-server zijn moet alleen tijdens een verbindingspoging die is gemaakt van een apparaat dat is niet binnen de geconfigureerde goedgekeurde IP-adressen vereist. 


## <a name="next-steps"></a>Volgende stappen

Als u meer informatie over voorwaardelijke toegang toolearn, Zie [voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access-azure-portal.md).

