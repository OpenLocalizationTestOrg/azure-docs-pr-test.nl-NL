---
title: aaaIntroduction toodevice management in Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe Apparaatbeheer kan u helpen tooget controle over het Hallo-apparaten die toegang hebben tot bronnen in uw omgeving.
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Inleiding toodevice management in Azure Active Directory

Azure Active Directory (Azure AD) kunnen in een wereld mobiel eerste, cloud eerste toodevices voor eenmalige aanmelding, apps en services vanaf elke locatie. IT-professionals worden met Hallo komst van apparaten - Bring Your Own Device (BYOD), inclusief momenteel geconfronteerd met twee tegengestelde doelstellingen:

- Hallo eindgebruikers toobe productief zorgen overal en wanneer
- Beveiligen van zakelijke activa Hallo op elk gewenst moment

Via apparaten wel uw gebruikers toegang tooyour zakelijke activa. tooprotect uw zakelijke activa als IT-beheerder wilt u toohave controle over deze apparaten. Hiermee kunt u ervoor dat uw gebruikers toegang hebben tot de bronnen vanaf apparaten die voldoen aan uw standaarden voor beveiliging en naleving toomake. 

Apparaatbeheer is ook Hallo fundering voor [voorwaardelijke toegang op basis van apparaten](active-directory-conditional-access-policy-connected-applications.md). Met voorwaardelijke toegang op basis van apparaten, kunt u ervoor zorgen dat toegang tooresources in uw omgeving alleen mogelijk met is vertrouwde apparaten.   

In dit onderwerp wordt uitgelegd hoe beheer van apparaten in Azure Active Directory werkt.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Apparaten onder beheer van Azure AD Hallo laten

een apparaat onder het beheer van Azure AD Hallo tooget, hebt u twee opties:

- Registreren 
- Samenvoegen

**Registreren van** een apparaat tooAzure AD kunt u toomanage een apparaat-id. Wanneer een apparaat is geregistreerd, biedt Azure AD-apparaatregistratie Hallo-apparaat met een identiteit die is gebruikt tooauthenticate Hallo apparaat wanneer een gebruiker zich aanmeldt tooAzure AD. U kunt Hallo identiteit tooenable gebruiken of een apparaat uitschakelen.

In combinatie met een MDM-oplossing voor mobiele apparaten, zoals Microsoft Intune, worden Hallo apparaatkenmerken in Azure AD bijgewerkt met aanvullende informatie over het Hallo-apparaat. Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving. Zie voor meer informatie over de inschrijving van apparaten in Microsoft Intune, apparaten inschrijven voor beheer in Intune.

**Lid worden van** een apparaat is een uitbreiding tooregistering een apparaat. Dit betekent het geeft u alle Hallo voordelen van het registreren van een apparaat en in toevoeging toothis, ook invloed op Hallo van lokale status van een apparaat. Hallo lokale status wijzigen, kunt uw gebruikers toosign in tooa apparaat met een organisatie werk- of schoolaccount in plaats van een persoonlijk account.

## <a name="azure-ad-registered-devices"></a>Azure AD ingeschreven apparaten   

Hallo doel van Azure AD ingeschreven apparaten is tooprovide u met ondersteuning voor Hallo **Bring Your Own Device (BYOD)** scenario. In dit scenario wordt een gebruiker toegang krijgen tot bronnen van van uw organisatie Azure Active Directory die worden beheerd met behulp van een persoonlijk apparaat.  

![Azure AD ingeschreven apparaten](./media/device-management-introduction/03.png)

Hallo-toegang is gebaseerd op een account voor werk of school die is ingevoerd op Hallo-apparaat.  
Windows 10 kan bijvoorbeeld gebruikers tooadd een werk of school-account tooa pc, tablet of telefoon.  
Wanneer een gebruiker een werk- of schoolaccount, Hallo-apparaat is toegevoegd, is geregistreerd in Azure AD en eventueel ingeschreven in Hallo mobiele apparaten (MDM) beheersysteem dat uw organisatie is geconfigureerd. Gebruikers van uw organisatie kunnen toevoegen van een werk of school account tooa persoonlijk apparaat gemakkelijk:

- Bij het openen van een werktoepassing voor Hallo eerst
- Handmatig via Hallo **instellingen** menu in geval van Windows 10 Hallo 

U kunt Azure AD geregistreerde apparaten configureren voor Windows 10-, iOS-, Android- en Mac OS.

## <a name="azure-ad-joined-devices"></a>Azure AD die lid zijn van apparaten

Hallo-doel van Azure AD die lid zijn van apparaten is toosimplify:

- Windows-implementaties van apparaten die eigendom zijn van werkitems 
- Toegang tooorganizational apps en resources van een Windows-apparaat

![Azure AD ingeschreven apparaten](./media/device-management-introduction/02.png)


Deze doelstellingen worden bereikt door het verstrekken van uw gebruikers met een selfservice-ervaring voor het ophalen van apparaten die eigendom zijn van werk onder het Hallo-beheer van Azure AD.  
**Azure AD Join** is bedoeld voor organisaties die cloud eerste / alleen in de cloud. Dit zijn meestal kleine en middelgrote bedrijven die geen een on-premises Windows Server Active Directory-infrastructuur. 

Implementatie van Azure AD die lid zijn van apparaten biedt Hallo volgende voordelen:

- **Eenmalige aanmelding (SSO)** tooyour Azure beheerd SaaS-apps en services. Uw gebruikers zien geen extra authenticatie prompts bij het openen van bronnen op het werk. Hallo SSO-functionaliteit is zelfs wanneer ze niet verbonden toohello domeinnetwerk die beschikbaar zijn.

- **Enterprise compatibele roaming** van gebruikersinstellingen op gekoppelde apparaten. Gebruikers hoeven niet tooconnect een Microsoft-account (bijvoorbeeld Hotmail) toosee-instellingen op apparaten.

- **Toegang tot tooWindows Store voor bedrijven** met behulp van AD-account. Uw gebruikers kunnen kiezen uit een inventarisatie van toepassingen die vooraf zijn geselecteerd door Hallo-organisatie.

- **Windows Hello** ondersteuning voor beveiligde en gemakkelijke toegang tot toowork bronnen.

- **Beperking van toegang** tooapps van alleen de apparaten die voldoen aan nalevingsbeleid.

Terwijl Azure AD join is voornamelijk bedoeld voor organisaties waarvoor geen een on-premises Windows Server Active Directory-infrastructuur, kunt u gewoon ook worden gebruikt in scenario's waarbij:

- U kunt een domein lokale bijvoorbeeld niet gebruiken als u mobiele apparaten zoals tablets en telefoons onder controle tooget moet.

- Uw gebruikers moeten voornamelijk tooaccess Office 365 of andere SaaS-apps die is geïntegreerd met Azure AD.

- U wilt dat een groep gebruikers toomanage in Azure AD in plaats van in Active Directory. Dit kan van toepassing, bijvoorbeeld tooseasonal werknemers, contractanten of studenten.

- Wilt u gekoppelde mogelijkheden tooworkers tooprovide in externe filialen met beperkte on-premises infrastructuur.

U kunt Azure AD die lid zijn van apparaten voor Windows 10-apparaten kunt configureren.


## <a name="hybrid-azure-ad-joined-devices"></a>Hybride Azure AD die lid zijn van apparaten

Voor meer dan een tien jaar hebben veel organisaties Hallo domain join tootheir lokale Active Directory tooenable gebruikt:

- IT-afdelingen toomanage werk-apparaten die eigendom zijn van een centrale locatie.

- Gebruikers toosign in tootheir apparaten met hun Active Directory werk- of schoolaccounts. 

Normaal gesproken organisaties met een lokale footprint afhankelijk zijn van installatiekopieën van de methoden tooprovision apparaten en kunnen ze vaak gebruiken **System Center Configuration Manager (SCCM)** of **Groepsbeleid (GP)** toomanage ze.

Als uw omgeving een on-premises AD-footprint en ook voordeel van het Hallo-mogelijkheden van Azure Active Directory, kunt u hybride Azure AD die lid zijn van apparaten implementeren. Dit zijn apparaten die beide zijn, gekoppelde tooyour lokale Active Directory en uw Azure Active Directory.

![Azure AD ingeschreven apparaten](./media/device-management-introduction/01.png)


Gebruik Azure AD hybride die lid zijn van apparaten als:

- U hebt Win32-apps geïmplementeerde toothese apparaten die gebruikmaken van NTLM / Kerberos.

- Gewenste GP of SCCM / DCM toomanage apparaten.

- U wilt dat toocontinue toouse imaging oplossingen tooconfigure apparaten voor uw werknemers.

U kunt configureren hybride Azure AD die lid zijn van apparaten voor Windows 10 en downlevel-apparaten, zoals Windows 8 en Windows 7.

## <a name="summary"></a>Samenvatting

Met Apparaatbeheer in Azure AD, kunt u het volgende doen: 

- Hallo vereenvoudigen van apparaten meebrengen onder het Hallo-beheer van Azure AD

- Uw gebruikers voorzien van een eenvoudig toouse toegang tooyour organisatie cloud-gebaseerde bronnen

Als een regel van een miniatuur, moet u het volgende gebruiken:

- Azure AD geregistreerde apparaten voor persoonlijke apparaten

- Azure AD die lid zijn van apparaten voor apparaten die niet lid tooan on-premises AD dat 

- Hybride Azure AD die lid zijn van apparaten voor apparaten die zijn gekoppeld tooan on-premises AD dat     




## <a name="next-steps"></a>Volgende stappen

- een overzicht van hoe toomanage apparaat in Azure portal, Zie Hallo tooget [apparaten beheert met hello Azure-portal](device-management-azure-portal.md)

- toolearn meer informatie over voorwaardelijke toegang op basis van apparaten, Zie [Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren](active-directory-conditional-access-policy-connected-applications.md).

- toosetup hybride Azure AD die lid zijn van apparaten, Zie [hoe tooconfigure hybride Azure Active Directory apparaten samengevoegd](device-management-hybrid-azuread-joined-devices-setup.md).


