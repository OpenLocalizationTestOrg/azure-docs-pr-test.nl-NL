---
title: aaaHow tooconfigure automatische registratie van Windows-domein-apparaten met Azure Active Directory | Microsoft Docs
description: Instellen van uw domein Windows-apparaten tooregister automatisch en zonder tussenkomst met Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Aan de slag met Azure Active Directory-apparaatregistratie

Azure Active Directory-apparaatregistratie vormt de basis Hallo voor scenario's voor voorwaardelijke toegang op basis van apparaten. Wanneer een apparaat is geregistreerd, biedt Azure Active Directory-apparaatregistratie Hallo-apparaat met een identiteit die gebruikt tooauthenticate Hallo apparaat is wanneer Hallo gebruiker zich aanmeldt. vervolgens Hallo geverifieerde apparaat en Hallo kenmerken van Hallo-apparaat, kunnen de gebruikte tooenforce beleidsregels voor voorwaardelijke toegang voor toepassingen die worden gehost in Hallo cloud en on-premises worden.

In combinatie met een MDM-oplossing voor mobiele apparaten, zoals Microsoft Intune, worden Hallo apparaatkenmerken in Azure Active Directory bijgewerkt met aanvullende informatie over het Hallo-apparaat. Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving. Zie voor meer informatie over de inschrijving van apparaten in Microsoft Intune, apparaten inschrijven voor beheer in Intune.
Mogelijke scenario's met Azure Active Directory apparaat registratie Azure Active Directory-apparaatregistratie biedt ondersteuning voor iOS, Android en Windows apparaten. afzonderlijke scenario's voor een Hallo die gebruikmaken van Azure AD-apparaatregistratie gelden mogelijk meer specifieke vereisten en platformondersteuning. 

Het gaat om de volgende scenario's:

- **Voorwaardelijke toegang voor Office 365-toepassingen met Microsoft Intune:** IT-beheerders kunnen voorwaardelijke toegang apparaat beleid toosecure bedrijfsbronnen, inrichten terwijl op Hallo dezelfde toestaan informatiemedewerkers op compatibele apparaten tijdstip tooaccess Hallo-services. Zie Conditional Access Device Policies for Office 365 services (Engelstalig) voor meer informatie.

- **Voorwaardelijke toegang tooapplications die worden gehost op de lokale:** kunt u geregistreerde apparaten met toegangsbeleid voor toepassingen die zijn geconfigureerd toouse AD FS met Windows Server 2012 R2. Zie [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](active-directory-device-registration-on-premises-setup.md) (Engelstalig) voor meer informatie over het instellen van on-premises voorwaardelijke toegang.

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory-apparaatregistratie configureren

apparaatregistratie toosetup, hebt u meerdere opties:

- Apparaten kunnen registreren wanneer samengevoegde tooAzure AD-domein. Voor meer informatie over dit onderwerp kunt u meer informatie over Azure AD Join en Hallo instellingen die vereist zijn voor gebruikers toojoin Azure AD-domein.

- Apparaten kunnen worden geregistreerd wanneer gebruikers werk voegen of school tooWindows accounts op een persoonlijk apparaat, of wanneer u mobiele apparaten verbinding maken met bronnen op het werk tooa registratie vereisen. tooensure, moet u Azure AD-apparaatregistratie in Azure Portal Hallo inschakelen. 

- Apparaten kunnen worden geregistreerd met behulp van automatische apparaatregistratie voor traditionele domein-machines. tooensure, moet u eerst Setup Azure AD Connect voordat u met automatische apparaatregistratie doorgaat.

Zie voor instructies nieuwste [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).  
U kunt ook bekijken en inschakelen of uitschakelen van de geregistreerde apparaten met Hallo Beheerdersportal in Azure Active Directory.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Hello Azure Active Directory device registration-service inschakelen

**tooenable hello Azure Active Directory device registration-service:**

1.  Meld u toohello Microsoft Azure-portal als administrator.

2.  Selecteer in het linkerdeelvenster Hallo **Active Directory**.

3.  Tabblad Hallo-map, selecteer uw directory.

4.  Klik op **Configureren**

5.  Schuif te**apparaten**.

6.  Alles selecteren voor gebruikers kan hun apparaten REGISTREREN met AZURE AD.

7.  Selecteer Hallo maximum aantal apparaten dat u wilt dat tooauthorize per gebruiker.

Hallo registratie bij Microsoft Intune of Mobile Device Management voor Office 365 is apparaatregistratie vereist. Als u een van deze services hebt geconfigureerd **alle** is geselecteerd en **** is uitgeschakeld. Zorg ervoor dat ze juist zijn geconfigureerd en Hallo geschikte licenties hebt.

Verificatie met twee factoren is standaard niet ingeschakeld voor Hallo-service. Deze vorm van verificatie wordt echter wel aanbevolen bij het registreren van een apparaat.

- Voordat u verificatie met twee factoren voor deze service, moet u een provider voor verificatie met twee factoren configureren in Azure Active Directory en uw gebruikersaccounts configureren voor meervoudige verificatie, Zie multi-factor Authentication toevoegen tooAzure Active Directory

- Als u gebruikmaakt van AD FS met Windows Server 2012 R2, moet u een module verificatie met twee factoren configureren in AD FS, Zie multi-factor Authentication gebruiken met Active Directory Federation Services.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Apparaatobjecten bekijken en beheren in Azure Active Directory

Vanuit de Hallo beheerder van de Azure portal kunt u weergeven, blokkeren en blokkering van apparaten. Een apparaat dat is geblokkeerd hoeft niet langer toegang tooapplications die geconfigureerd tooallow alleen geregistreerde apparaten zijn.

**tooview en apparaatobjecten in Azure Active Directory beheren:**
 
1.  Meld u aan toohello Microsoft Azure-portal als beheerder.

2.  Selecteer in het linkerdeelvenster Hallo **Active Directory**.

3.  Selecteer uw directory.

4.  Selecteer **gebruikers**. 

5.  Klik op Hallo gebruiker waarvoor u wilt dat toosee Hallo apparaten.

6.  Selecteer **apparaten**.

7.  Selecteer **apparaten geregistreerd**.

U kunt nu controleren, blokkeren of deblokkeren van gebruiker Hallo geregistreerde apparaten.
Windows 10-apparaten die zich on-premises domein en automatisch worden geregistreerd, worden niet weergegeven onder het tabblad Hallo-gebruikers. Gebruik Hallo Get MsolDevice PowerShell-opdracht toofind alle apparaten in uw onderneming. 


## <a name="next-steps"></a>Volgende stappen

toosetup automatische apparaatregistratie, Zie [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).


