---
title: een Azure hybride identiteitsoplossing aaaChoose | Microsoft Docs
description: Haal een basiskennis van Hallo beschikbare hybride identiteitsoplossingen en aanbevelingen voor u toomake Hallo beste identiteit governance beslissing voor uw organisatie.
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Microsoft-oplossingen voor hybride identiteit
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) hybride identiteitsoplossingen kunnen u toosynchronize on-premises mapobjecten met Azure AD tijdens nog steeds het beheren van uw gebruikers on-premises. Hallo eerste beslissing toomake bij het plannen van uw lokale Windows Server Active Directory met Azure AD is of u wilt toouse identiteit gesynchroniseerd of federatieve identiteit toosynchronize. Gesynchroniseerde identiteiten en eventueel wachtwoord-hashes, kunnen uw gebruikers toouse Hallo tooaccess met hetzelfde wachtwoord zowel on-premises en organisatie-cloudresources. Voor meer geavanceerde scenariovereisten op, zoals het eenmalige aanmelding (SSO) of lokale MFA, moet u toodeploy Active Directory Federation Services (AD FS) toofederate identiteiten. 

Er zijn diverse opties beschikbaar voor het configureren van hybride identiteit. Dit artikel bevat informatie toohelp die u Hallo beste één voor uw organisatie op basis van een eenvoudig te implementeren en uw specifieke identiteits- en toegangsbeheer-beheer moet kiezen. Als u welk identiteitsmodel u het beste past bij de behoeften van uw organisatie overweegt, moet u ook toothink over tijd, de bestaande infrastructuur, de complexiteit en kosten. Deze factoren zijn voor elke organisatie anders en na verloop van tijd kunnen wijzigen. Als uw vereisten veranderen, wel u ook Hallo flexibiliteit tooswitch tooa andere identiteitsmodel.

> [!TIP]
> Deze oplossingen worden geleverd door [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Gesynchroniseerde identiteiten 
Gesynchroniseerde identiteit is de eenvoudigste manier toosynchronize Hallo lokale directory-objecten (gebruikers en groepen) met Azure AD. 

![Gesynchroniseerde hybride identiteit](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Gesynchroniseerde identiteiten is de eenvoudigste en snelste methode hello, moeten uw gebruikers nog steeds toomaintain een afzonderlijk wachtwoord voor cloud-gebaseerde bronnen. tooavoid, u kunt ook (optioneel) [een hash van gebruikerswachtwoorden synchroniseren](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) tooyour Azure AD-directory. Synchroniseren van de wachtwoord-hashes kunnen gebruikers toolog in op basis van toocloud organisatieresources met Hallo dezelfde gebruikersnaam en wachtwoord dat ze lokale gebruiken. Azure AD Connect controleert periodiek uw on-premises directory op wijzigingen en houdt uw Azure AD-directory worden gesynchroniseerd. Wanneer een gebruikerskenmerk of het wachtwoord gewijzigd op lokale Active Directory is, wordt deze automatisch bijgewerkt in Azure AD. 

Voor de meeste organisaties die alleen hun gebruikers toosign in tooOffice 365, SaaS-toepassingen en andere Azure AD gebaseerde-resources tooenable moeten wordt Hallo standaard wachtwoord synchronisatieoptie aanbevolen. Als dat niet werkt, moet u toodecide tussen Pass through-verificatie en AD FS.

> [!TIP]
> Wachtwoorden van gebruikers worden opgeslagen in de lokale Windows Server Active Directory in Hallo vorm van een hashwaarde die de werkelijke gebruikerswachtwoord Hallo vertegenwoordigt. Een hash-waarde is een resultaat van een wiskundige eenrichtingsfunctie (hello hash-algoritme). Er is geen methode toorevert Hallo resultaat van een one-way function toohello tekst zonder opmaak versie van een wachtwoord. U kunt een wachtwoord-hash-toosign in tooyour on-premises netwerk gebruiken. Wanneer u ervoor kiezen wachtwoorden toosynchronize, Azure AD Connect uitgepakt wachtwoord-hashes van Hallo on-premises Active Directory en extra beveiliging toohello wachtwoordhash verwerken voordat deze gesynchroniseerde tooAzure AD is van toepassing is. Wachtwoordsynchronisatie kan ook worden gebruikt samen met wachtwoord terugschrijven tooenable selfservice wachtwoordherstel in Azure AD. U kunt bovendien eenmalige aanmelding (SSO) inschakelen voor gebruikers van domeincomputers die verbonden toohello bedrijfsnetwerk zijn. Met eenmalige aanmelding moeten ingeschakelde gebruikers alleen tooenter een gebruikersnaam toosecurely toegang tot cloud-bronnen. 

## <a name="pass-through-authentication"></a>Pass through-verificatie
[Azure AD Pass-through-verificatie](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) biedt een eenvoudig wachtwoord validatie-oplossing voor Azure AD gebaseerde services met behulp van uw lokale Active Directory. Als beveiliging en naleving van beleid voor uw organisatie niet is toegestaan voor het verzenden van wachtwoorden van gebruikers, zelfs in een formulier hash en u alleen toosupport bureaublad SSO voor apparaten die lid zijn van een domein hoeft, is het raadzaam dat u evalueren met behulp van Pass through-verificatie. Pass through-verificatie is niet vereist voor elke implementatie in Hallo DMZ die Hallo implementatie-infrastructuur in vergelijking met AD FS vereenvoudigt. Wanneer gebruikers zich met behulp van Azure AD aanmelden, valideert deze verificatiemethode rechtstreeks op uw lokale Active Directory-wachtwoorden van gebruikers.

![Pass through-verificatie](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Met Pass through-verificatie is niet nodig voor een complexe netwerkinfrastructuur en u hoeft niet toostore on-premises wachtwoorden in Hallo cloud. In combinatie met eenmalige aanmelding Pass through-verificatie biedt een volledig geïntegreerde ervaring als u zich aanmeldt tooAzure AD of andere cloudservices.

Pass through-verificatie is geconfigureerd met Azure AD Connect, dat gebruikmaakt van een eenvoudige lokale agent die naar aanvragen voor wachtwoord-validatie luistert. Hallo-agent worden eenvoudig geïmplementeerde toomultiple machines tooprovide hoge beschikbaarheid en taakverdeling. Aangezien alle communicatie alleen uitgaand zijn, is er geen vereiste voor Hallo connector toobe geïnstalleerd in een Perimeternetwerk. Hallo server computervereisten voor Hallo-connector zijn als volgt:

- Windows Server 2012 R2 of hoger
- Lid van domein tooa in Hallo forest waarmee gebruikers worden gevalideerd

> [!NOTE]
> Azure AD Pass-through-verificatie is momenteel in preview en wordt ondersteund voor web browser gebaseerde clients en Office-clients die moderne verificatie ondersteunen. Voor clients die niet worden ondersteund, zoals oudere Office-clients en Exchange ActiveSync (inclusief systeemeigen e-mailclients op mobiele apparaten), is het aanbevolen toouse Hallo moderne verificatie equivalent. Moderne verificatie wordt niet alleen kan Pass through-verificatie, maar er wordt een biedt tevens mogelijkheden voor voorwaardelijk beleid toobe toegepast, zoals multi-factor authentication-server. 

Pass through-verificatie is momenteel niet ondersteund wanneer met behulp van Windows 10-apparaten die lid zijn van tooAzure AD. Echter kunt u synchronisatie van wachtwoordhash gebruiken als een automatische terugval toosupport Windows 10 en verouderde clients van Hallo eerder is vermeld. Tijdens het Hallo-preview synchronisatie van wachtwoordhash standaard ingeschakeld wanneer Pass through-verificatie is geselecteerd als Hallo aanmeldoptie in Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Federatieve identiteiten (AD FS)
Voor meer controle over hoe gebruikers toegang Office 365 en andere cloudservices tot, kunt u instellen van directorysynchronisatie met het gebruik van eenmalige aanmelding (SSO) [Active Directory Federation Services (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Federatie van uw gebruikers aanmeldingen met AD FS gemachtigden verificatie tooan op de lokale server te valideren en gebruikersreferenties. In dit model worden on-premises Active Directory-referenties nooit tooAzure AD doorgegeven.

![Federatieve identiteiten](./media/choose-hybrid-identity-solution/federated-identity.png)

Ook wel identiteitsfederatie genoemd, deze methode aanmelden zorgt ervoor dat alle gebruikersverificatie gecontroleerde on-premises en kan beheerders tooimplement strengere niveaus van toegangsbeheer. Identiteitsfederatie met AD FS is Hallo meest ingewikkeld optie en implementatie van extra servers in uw on-premises omgeving is vereist. Identiteitsfederatie voert u ook tooproviding 24 x 7 ondersteuning voor uw Active Directory en AD FS-infrastructuur. Deze hoge mate van ondersteuning is nodig omdat als uw Internet-lokale toegang, domeincontroller of AD FS-servers niet beschikbaar zijn, gebruikers zich niet aanmelden toocloud services.

> [!TIP]
> Als u besluit toouse Federatie met Active Directory Federation Services (AD FS), kunt u desgewenst instellen Wachtwoordsynchronisatie als een back-up als uw AD FS-infrastructuur is mislukt.


## <a name="common-scenarios-and-recommendations"></a>Algemene scenario's en aanbevelingen
Hier volgen enkele algemene hybride identiteit en toegang beheerscenario's met aanbevelingen als toowhich hybride identiteitsoptie (of opties) mogelijk geschikt voor elk.

|Ik wil:|PWS en SSO<sup>1</sup>| PTA en SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Nieuwe gebruiker, contactpersonen en groepsaccounts die zijn gemaakt in Mijn lokale Active Directory toohello cloud automatisch synchroniseren.|![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png) |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Instellen van mijn tenants voor Office 365 hybride scenario 's|![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png) |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Mijn gebruikers toosign in te schakelen en toegang tot cloudservices met hun on-premises-wachtwoord|![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png) |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Eenmalige aanmelding met bedrijfsreferenties implementeren|![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)| ![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png) |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Zorg ervoor dat er geen wachtwoord-hashes zijn opgeslagen in de cloud Hallo| |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Oplossingen voor on-premises meervoudige verificatie inschakelen| | |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Smartcardverificatie ondersteuning voor Mijn gebruikers<sup>4</sup>| | |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|
|Wachtwoord verlopen-meldingen weergegeven in Hallo Office-Portal en op Hallo Windows 10 desktop| | |![Aanbevolen](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Wachtwoordsynchronisatie met eenmalige aanmelding. 

> <sup>2</sup> Pass through-verificatie en eenmalige aanmelding. 

> <sup>3</sup> federatieve eenmalige aanmelding met AD FS.

> <sup>4</sup> AD FS kan worden geïntegreerd met uw enterprise PKI tooallow aanmelden met behulp van certificaten. Deze certificaten kunnen worden soft-certificaten die zijn geïmplementeerd via vertrouwde inrichting kanalen zoals MDM of GPO of smartcard-certificaten (inclusief PIV/CAC kaarten) of Hello voor bedrijven (cert-vertrouwensrelatie). Zie voor meer informatie over ondersteuning voor smartcard-verificatie, [deze blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Volgende stappen
[Meer informatie in een omgeving met Azure Proof-of-Concept](https://aka.ms/aad-poc)

[Azure AD Connect installeren](http://go.microsoft.com/fwlink/?LinkId=615771)

[Synchronisatie van hybride identiteit controleren](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

