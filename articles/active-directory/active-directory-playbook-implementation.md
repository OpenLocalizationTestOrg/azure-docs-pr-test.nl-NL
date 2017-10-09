---
title: Active Directory-implementatiemodel Playbook implementatie aaaAzure | Microsoft Docs
description: Verkennen en snel implementeren scenario's voor Identity and Access Management
services: active-directory
keywords: Azure active directory, playbook, Proof-of-Concept, implementatiemodel
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Azure Active Directory-bewijs van Concept Playbook: uitvoering

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - AD tooAzure AD synchroniseren 

Een hybride identiteit is Hallo basis voor de meeste Hallo enterprise-klanten die al een on-premises adreslijst hebben. Hallo hier de doelstelling is toointentionally als minder tijd hier mogelijk tooshow Hallo-waarde van Hallo werkelijke identiteit en toegang scenario's. 

| Scenario | Bouwstenen| 
| --- | --- |  
| [Uw on-premises uitbreiden identity toohello cloud](#extending-your-on-premises-identity-to-the-cloud) | [Synchronisatie van Directory - Wachtwoordhashsynchronisatie](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Opmerking**: als u al DirSync/ADSync of eerdere versies van Azure AD Connect hebt, deze stap is optioneel. Sommige scenario's in deze handleiding mogelijk nieuwere versie van Azure AD Connect.  <br/>[De huisstijl](active-directory-playbook-building-blocks.md#branding) | 
| [Groepen met Azure AD-licenties toewijzen](#assigning-azure-ad-licenses-using-groups) | [Groeperen op basis van de licentieverlening](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Uw on-premises uitbreiden identity toohello cloud 

1. Bob is Hallo Active Directory-beheerder bij Contoso. Hij Hallo vereiste tooenable identiteit opgehaald als een service voor een groep gebruikers. Hallo identiteit van de beschikbare Hallo Doelgebruikers in de cloud Hallo na de uitvoering van Azure AD Connect-wizard. 
2. Bob vraagt Susie een Doelgebruikers hello, tooaccess hello Azure Active Directory-Toegangsvenster en Bevestig dat ze kan worden geverifieerd. Susie ziet een huisstijl aanmeldingspagina en een leeg Toegangsvenster die gereed is voor het inschakelen van toegang voor toekomstige toepassingen.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Groepen met Azure AD-licenties toewijzen 

1. Bob is Hallo globale beheerder van Azure AD en wil tooallocate Azure AD-licenties tooa specifieke set met gebruikers als onderdeel van de initiële implementatie Hallo van Azure AD.
2. Bob maakt een groep voor Hallo testgebruikers. 
3. Bob wijst Hallo licenties toohello groep
4. Susie een Hallo informatiemedewerkers, wordt toohello beveiligingsgroep toegevoegd als onderdeel van haar taakfuncties
5. Na enige tijd heeft Susie toegang toohello Azure AD premium-licentie. Hiermee schakelt u meer Hallo Implementatiemodel scenario's later op.

## <a name="theme---lots-of-apps-one-identity"></a>Thema - veel apps, één identiteit

| Scenario | Bouwstenen| 
| --- | --- |  
| [Het integreren van SaaS-toepassingen - federatieve SSO](#integrate-saas-applications---federated-sso) | [Configuratie van de SaaS-federatieve SSO](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Groepen - overgedragen eigendom](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Wachtwoord eenmalige aanmelding voor SaaS-toepassingen - integreren](#integrate-saas-applications---password-sso) | [SaaS-wachtwoord SSO-configuratie](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [Eenmalige aanmelding en Identity Lifecycle Events](#sso-and-identity-lifecycle-events) | [SaaS en Identity Lifecycle](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Toegangsaccounts tooShared beveiligen](#secure-access-to-shared-accounts) | [SaaS gedeelde configuratie van Accounts](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Externe toegang tooOn-Premises toepassingen beveiligen](#secure-remote-access-to-on-premises-applications) | [App-proxyconfiguratie](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [LDAP-identiteiten tooAzure AD synchroniseren](#synchronize-ldap-identities-to-azure-ad) |  [Algemene configuratie van de LDAP-Connector](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Het integreren van SaaS-toepassingen - federatieve SSO 

1. Bob hello Azure AD met globale beheerder is en een aanvraag ontvangt van Hallo Marketing afdeling tooenable toegang tootheir ServiceNow-exemplaar. Bob Hallo stapsgewijze zelfstudie zoekt in de documentatie van Azure AD en erna en gemachtigden Hallo toewijzing van gebruikers toohello app tooKevin, Hallo-head van Marketing-team. 
2. Kevin zich aanmeldt als Hallo eigenaar van rechten tussen ServiceNow en Susie toohello app wijst. Kevin ook meldingen van Susie profiel automatisch in ServiceNow is gemaakt
3. Susie is een Informatiemedewerker in de marketingafdeling Hallo. Ze worden vastgelegd in tooazure AD en vindt alle SaaS-toepassingen is ze tooin myapps portal toegewezen. Van daaruit ze naadloos toegang tooServiceNow opgehaald.
4. Hallo marketingafdeling wil tooaudit die ServiceNow toegang heeft. Bob downloadt van een activiteitenrapport en wordt gedeeld met Kevin via e-mail.  

### <a name="sso-and-identity-lifecycle-events"></a>Eenmalige aanmelding en Identity Lifecycle Events

1. Susie duurt een laat afwezig, en door het bedrijfsbeleid Hallo on-premises AD-account is tijdelijk uitgeschakeld. Susie nu niet kunt aanmelden tooAzure AD en daarom geen toegang tot ServiceNow. 
2. Susie maakt een laterale verplaatsing van tooSales Marketing. Kevin verwijderd haar toegang uit ServiceNow. Susie wordt geregistreerd in azure ad-myapps hello en ze niet langer Hallo ServiceNow-tegel ziet. Na 10 minuten bevestigt Kevin dat Susie account is uitgeschakeld in ServiceNow-beheerconsole.

### <a name="integrate-saas-applications---password-sso"></a>Wachtwoord eenmalige aanmelding voor SaaS-toepassingen - integreren

1. Bob configureert toegang tooAtlassian HipChat. HipChat heeft tooSusie van wachtwoord SSO-integratie en Verleen toegang
2. Susie toohello myapps portal aanmeldt en ziet een koppeling toodownload hello Azure AD-IE browser extensie, die ze downloadt
3. Wanneer u op klikt, ze opgehaald haar HipChat gebruikersnaam en wachtwoord om referenties gevraagd. Dit is een eenmalige bewerking en na het voltooien van deze ze tooHipChat toegang heeft
4. Een paar dagen later Susie myapps portal en klikt op HipChat opnieuw. Dit keer ongeveer krijgt ze deze naadloos toegang
5. Kevin, Hallo HipChat app eigenaar wil tooaudit die toepassing hello toegang heeft. Bob een controlerapport downloadt en gedeeld met Kevin via e-mail. 

### <a name="secure-access-tooshared-accounts"></a>Toegangsaccounts tooShared beveiligen 

1. Bob is toosecure te beheren Hallo gedeeld Twitter-ingang voor leden van Hallo Sales-team. Hij voegt Twitter toe als een SSO-toepassing en toegewezen toohello beveiligingsgroep Hallo Sales-Team. Hij Hallo referenties toohello gedeeld account is opgegeven en hij deze voorziet in Hallo-systeem. 
2. Referenties voor Twitter delen wordt niet meer vertrouwd vanwege toomultiple mensen die zijn geïnstalleerd. Bob kan automatische rollover van Hallo Twitter-wachtwoord.
3. Susie, lid zijn van Hallo Sales-team, toohello myapps portal aanmeldt en een koppeling toodownload hello Azure AD-IE Browseruitbreiding ziet. Ze worden geïnstalleerd.
4. Wanneer u op klikt ze get rechtstreeks toegang hebben tot tooTwitter. Ze weet niet Hallo wachtwoord.
5. Arnold maakt ook deel uit van het verkoopteam Hallo. Hij heeft Hallo dezelfde ervaring als Susie in stap 3 en 4
6. Hallo verkoopafdeling wil tooaudit die Twitter toegang heeft. Bob downloadt van een activiteitenrapport en wordt gedeeld met Kevin via e-mail. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Externe toegang tooOn-Premises toepassingen beveiligen

1. Berend hello Azure AD globale beheerder is verbeterd talrijke verzoeken tooenable werknemers tooaccess diverse nuttig lokale bronnen, zoals Hallo uitgaven toepassing tijdens het op afstand werken. Hij volgt Hallo [toepassingsproxy documentatie](active-directory-application-proxy-enable.md) tooinstall een connector en onkosten publiceren als een toepassing Application Proxy. 
2. Hallo externe uitgaven toepassing URL delen Bob met Susie een Hallo werknemers die extern toegang nodig heeft. Ze toegang heeft tot Hallo koppeling en na verificatie ten opzichte van AAD, ze kunnen tooaccess Hallo uitgaven app en toobe productief blijven terwijl deze extern is. 
3. Bob wordt vervolgens doorgaat toopublish extra on-premises toepassingen via Hallo hetzelfde proces en geeft toegang tot toousers indien nodig. Hij voegt voorwaardelijke toegang en multi-factor authentication voor Hallo gevoeliger toepassingen die hij publiceert, tooensure extra beveiliging.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>LDAP-identiteiten tooAzure AD synchroniseren

1. Berend van het bedrijf heeft complexe identiteitsinfrastructuur kunt koppelen. De meeste Hallo gebruikers worden beheerd in Windows Server Active Directory Domain Services (toevoegen). Sommige van hen worden beheerd door HR-systeem in Active Directory Lightweight Directory Services (ADLDS).
2. Bob opgedragen toegang tooSaaS apps voor alle gebruikers (ook deze niet aanwezig in ADDS) inschakelen.
3. Algemene LDAP-Connector toopull gegevens uit ADLDS configureert Bob in Azure AD Connect.
4. Bob maakt synchronisatieregels zodat gebruikers LDAP zijn ingevuld in de Metaverse en tooAzure AD
5. Susie wordt LDAP gebruiker toegang krijgt tot haar SaaS app met behulp gesynchroniseerd identiteit



> [!IMPORTANT] 
> Dit is een geavanceerde configuratie vereisen enigszins bekend bent met FIM/MIM. Als het gebruikt in productie, wordt geadviseerd de vragen over deze configuratie gaat via [Premier Support](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Thema - verhoging van de beveiliging van uw 

| Scenario | Bouwstenen| 
| --- | --- |  
| [Beveiligde administrator-accounttoegang](#secure-administrator-account-access) | [Azure MFA met telefoongesprekken](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Veilige toegang voor toepassingen](#secure-access-to-applications) | [Voorwaardelijke toegang voor SaaS-toepassingen](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Alleen In de Time-beheer inschakelen](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Identiteiten op basis van de risico's beschermen](#protect-identities-based-on-risk) | [Risico's detecteren](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Aanmelden risico beleid implementeren](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Verifiëren zonder verificatie op basis van wachtwoorden](#authenticate-without-passwords-using-certificate-based-authentication) | [Gebaseerde certificaatverificatie configureren](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Beveiligde administrator-accounttoegang

1. Bob is Hallo hoofdbeheerder voor Azure AD. Hij is Stuart als medebeheerder van Hallo-service geïdentificeerd. 
2. Bob configureert van Stuart account tooalways MFA tooimprove hello beveiligingspostuur vereisen
3. Stuart wordt geregistreerd in Azure-portal toohello en kennisgevingen die hij nodig heeft tooregister zijn phone nummer toocontinue Hallo aanmelding
4. Toekomstige aanmeldingen van Stuart nu zijn beveiligd met meervoudige verificatie en hij nu ontvangt een telefoongesprek tooverify zijn identiteit.

### <a name="secure-access-tooapplications"></a>Veilige toegang tooapplications

1. Kevin is Hallo zakelijke eigenaar van ServiceNow. Hallo bedrijf wil nu die gebruikers toologin met MFA bij het openen van externe Hallo bedrijfsnetwerk.
2. Berend onze globale beheerder van Azure AD, voegt een voorwaardelijk beleid toohello ServiceNow toepassing tooenable MFA voor externe toegang
3. Susie, onze Informatiemedewerker wordt geregistreerd in de portal van mijn apps en klikt op Hallo ServiceNow-tegel. Ze is nu gecontroleerd met MFA.

### <a name="enable-just-in-time-jit-administration"></a>Just in time (Just in time)-beheer inschakelen

1. Bob en Stuart zijn globale beheerders van Azure AD. Ze willen tooenable JIT toegang toohello-beheerrollen en ook tookeep records op Hallo gebruik van Hallo beschermde rollen.
2. Bob PIM kan in hello Azure AD-tenant en wordt de beveiligingsbeheerder Hallo. Hij verandert zelf en lidmaatschap van de rol globale beheerder van Stuart van permanente tooeligible.
3. Bob en Stuart vereisen nu activeren van hun rol via hello Azure-portal voordat tooAzure AD als volgt wijzigt configuratie. 

### <a name="protect-identities-based-on-risk"></a>Identiteiten op basis van de risico's beschermen 

1. Susie, probeert een Informatiemedewerker logboekregistratie in een tor-browser. 
2. Bob hello Azure AD identity protection-dashboard controleert en Susie van aanmelding vanuit een anoniem IP-adres krijgt. Hallo beveiligingsteam wil toochallenge dergelijke heeft toegang tot gebruikers met MFA
3. Bob kan Azure AD Identity Protection-beleid toochallenge MFA voor gemiddeld of hoger risico 's
4. Tijd gaat door, en Susie in vanuit de browser Tor opnieuw. Deze tijd die ze zien Hallo MFA uitdaging

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Verifiëren zonder verificatie op basis van wachtwoorden

1. Bob is een globale beheerder voor financiële instelling, die gebruik van wachtwoorden als een factor authentication voor hun toepassingen verbiedt.
2. Bob kunt en dwingt certificaatverificatie op AD FS en Azure AD
3. Susie tijdens het openen van toepassing is gevraagd tooauthenticate met certificaat

## <a name="theme---scale-with-self-service"></a>Thema - schaal met selfservice

| Scenario | Bouwstenen| 
| --- | --- |  
| [Selfservice voor wachtwoordherstel](#self-service-password-reset) | [Selfservice voor wachtwoordherstel](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Self Servicetoegang tooApplications](#self-service-access-to-applications) | [Self Servicetoegang tooApplications](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Selfservice voor wachtwoordherstel 

1. Bob is hello Azure AD globale beheerder en schakelt Self Service wachtwoordbeheer tooa subset van gebruikers, met inbegrip van Susie. 
2. Susie registreert in toomyapps portal en zien een bericht tooregister haar beveiligingsinformatie voor toekomstige wachtwoord opnieuw instellen voor gebeurtenissen.
3. Snel vooruit een paar dagen Susie haar wachtwoord vergeet, en stelt deze via Azure AD-portal

### <a name="self-service-access-tooapplications"></a>Self Servicetoegang tooApplications 

1. Kevin is Hallo zakelijke eigenaar van ServiceNow. Hij wil dat gebruikers te 'aanmelden' voor het op aanvraag, in plaats van ze toe te voegen in één keer
2. Berend onze globale beheerder Azure AD wijzigt Hallo ServiceNow toepassing tooenable Self-service aanvragen
3. Susie, onze Informatiemedewerker wordt geregistreerd in de portal van mijn apps en klikt op knop 'Meer toepassingen toevoegen' Hallo en ServiceNow zien als een Hallo aanbevolen toepassingen. Vervolgens zij back toomy apps portal navigeert en ServiceNow-toepassing hello zien.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]