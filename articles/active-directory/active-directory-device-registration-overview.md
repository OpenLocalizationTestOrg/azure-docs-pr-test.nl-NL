---
title: overzicht van aaaAzure Active Directory device registration | Microsoft Docs
description: Azure Active Directory-apparaatregistratie vormt de basis Hallo voor scenario's voor voorwaardelijke toegang op basis van apparaten. Wanneer een apparaat is geregistreerd, Hallo voorziet in Azure Active Directory device registration-apparaat met een identiteit die gebruikt tooauthenticate Hallo apparaat is wanneer Hallo gebruiker zich aanmeldt.
services: active-directory
keywords: apparaatregistratie, apparaatregistratie inschakelen, apparaatregistratie en MDM
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Aan de slag met Azure Active Directory-apparaatregistratie
Azure Active Directory-apparaatregistratie vormt de basis Hallo voor scenario's voor voorwaardelijke toegang op basis van apparaten. Wanneer een apparaat is geregistreerd, biedt Azure Active Directory-apparaatregistratie Hallo-apparaat met een identiteit die gebruikt tooauthenticate Hallo apparaat is wanneer Hallo gebruiker zich aanmeldt. vervolgens Hallo geverifieerde apparaat en Hallo kenmerken van Hallo-apparaat, kunnen de gebruikte tooenforce beleidsregels voor voorwaardelijke toegang voor toepassingen die worden gehost in Hallo cloud en on-premises worden.

In combinatie met een MDM-oplossing voor mobiele apparaten, zoals Microsoft Intune, worden Hallo apparaatkenmerken in Azure Active Directory bijgewerkt met aanvullende informatie over het Hallo-apparaat. Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving. Zie [Apparaten inschrijven voor beheer in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune) voor meer informatie over het inschrijven van apparaten in Microsoft Intune.

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Mogelijke scenario's met Azure Active Directory-apparaatregistratie
Azure Active Directory-apparaatregistratie biedt ondersteuning voor iOS-, Android- en Windows-apparaten. afzonderlijke scenario's voor een Hallo die gebruikmaken van Azure AD-apparaatregistratie gelden mogelijk meer specifieke vereisten en platformondersteuning. Het gaat om de volgende scenario's:

* **Voorwaardelijke toegang tooapplications die worden gehost op de lokale**: U kunt geregistreerde apparaten met toegangsbeleid voor toepassingen die zijn geconfigureerd toouse AD FS met Windows Server 2012 R2. Zie [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](active-directory-device-registration-on-premises-setup.md) (Engelstalig) voor meer informatie over het instellen van on-premises voorwaardelijke toegang.
* **Voorwaardelijke toegang voor Office 365-toepassingen met Microsoft Intune** : IT-beheerders kunnen voorwaardelijke toegang apparaat beleid toosecure bedrijfsbronnen, inrichten terwijl op Hallo dezelfde toestaan informatiemedewerkers op compatibele apparaten tijdstip tooaccess Hallo-services. Zie [Conditional Access Device Policies for Office 365 services (Engelstalig)](active-directory-conditional-access-device-policies.md) voor meer informatie.

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory-apparaatregistratie configureren
U moet tooenable Azure AD-apparaatregistratie in hello Azure Portal, zodat mobiele apparaten Hallo-service detecteren kunnen door te zoeken naar bekende DNS-records. U moet uw bedrijfs-DNS configureren zodat Windows 10, Windows 8.1, Windows 7, Android en iOS-apparaten kunnen detecteren en Hallo-service gebruiken.
U kunt bekijken en geregistreerde apparaten met Hallo Beheerdersportal in Azure Active Directory in-of uitschakelen.

> [!NOTE]
> Voor de meest recente instructies over hoe tooset van automatische apparaatregistratie zien, [hoe toosetup automatische registratie van Windows-domein die lid zijn van apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>De service Azure Active Directory-apparaatregistratie inschakelen
1. Meld u toohello Microsoft Azure-portal als Administrator.
2. Selecteer in het linkerdeelvenster Hallo **Active Directory**.
3. Op Hallo **Directory** tabblad, selecteer uw directory.
4. Selecteer Hallo **configureren** tabblad.
5. Schuif toohello sectie **apparaten**.
6. Selecteer **ALLE** voor **GEBRUIKERS KUNNEN APPARATEN AAN WERKPLEK TOEVOEGEN**.
7. Selecteer Hallo maximum aantal apparaten dat u wilt dat tooauthorize per gebruiker.

> [!NOTE]
> Voor de inschrijving bij Microsoft Intune of Mobile Device Management voor Office 365 is Workplace Join vereist. Als u een van deze services hebt geconfigureerd, wordt alle geselecteerd en Hallo knop geen is uitgeschakeld.
> 
> 

Verificatie met twee factoren is standaard niet ingeschakeld voor Hallo-service. Deze vorm van verificatie wordt echter wel aanbevolen bij het registreren van een apparaat.

* Voordat u verificatie met twee factoren voor deze service, u moet een provider voor verificatie met twee factoren configureren in Azure Active Directory en uw gebruikersaccounts configureren voor meervoudige verificatie, Zie [multi-factor toe te voegen Verificatie tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Als u gebruikmaakt van AD FS met Windows Server 2012 R2, moet u een module voor verificatie met twee factoren configureren in AD FS. Zie [Using Multi-Factor Authentication with Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md) (Engelstalig).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Herkenning van Azure Active Directory-apparaatregistratie configureren
Windows 7 en Windows 8.1-apparaten worden gedetecteerd door Hallo device registration-service door een combinatie van Hallo gebruikersaccountnaam met de naam van een bekende apparaat registratie-server.

U moet een DNS CNAME-record dat toohello A-record die is gekoppeld met uw Azure Active Directory device registratieservice wijst maken. Hallo CNAME-record moet Hallo bekende voorvoegsel enterpriseregistration gevolgd door Hallo UPN-achtervoegsel dat wordt gebruikt door Hallo gebruikersaccounts in uw organisatie gebruiken. Gebruikt uw organisatie meerdere UPN-achtervoegsels, dan moeten er meerdere CNAME-records worden gemaakt in DNS.

Bijvoorbeeld, als u twee UPN-achtervoegsels gebruikt binnen uw organisatie met de naam @contoso.com en @region.contoso.com, maakt u Hallo DNS-records te volgen.

| Vermelding | Type | Adres |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Apparaatobjecten bekijken en beheren in Azure Active Directory
1. Vanuit de Hallo beheerder van de Azure portal kunt u weergeven, blokkeren en blokkering van apparaten. Een apparaat dat is geblokkeerd hoeft niet langer toegang tooapplications die geconfigureerd tooallow alleen geregistreerde apparaten zijn.
2. Toohello Microsoft Azure-Portal aanmelden als beheerder.
3. Selecteer in het linkerdeelvenster Hallo **Active Directory**.
4. Selecteer uw directory.
5. Selecteer Hallo **gebruikers** tabblad. Selecteer een gebruiker tooview op hun apparaten
6. Selecteer Hallo **apparaten** tabblad.
7. Selecteer **geregistreerde apparaten** van Hallo vervolgkeuzemenu.
8. Hier kunt u bekijken, blokkeren of deblokkeren van Hallo geregistreerde apparaten van gebruikers.

## <a name="additional-topics"></a>Extra onderwerpen
U kunt uw Windows 7- en Windows 8.1-apparaten die deelnemen aan een domein, registreren met Azure AD-apparaatregistratie. Hallo volgende onderwerpen vindt u meer informatie over Hallo vereisten en Hallo stappen vereist tooconfigure device registration op Windows 7 en Windows 8.1-apparaten.

* [Automatische apparaatregistratie bij Azure Active Directory voor Windows-apparaten die aan een domein deelnemen](active-directory-conditional-access-automatic-device-registration.md)
* [Automatic device registration with Azure Active Directory for Windows 10 domain-joined devices](active-directory-azureadjoin-devices-group-policy.md) (Automatische apparaatregistratie met Azure Active Directory voor Windows 10-apparaten die aan een domein deelnemen)

