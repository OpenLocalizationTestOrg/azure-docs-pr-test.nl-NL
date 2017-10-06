---
title: aaaFundamentals van Azure identiteitsbeheer | Microsoft Docs
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Grondbeginselen van Azure identity management
Meer digitale bedrijfsbronnen Live buiten Hallo bedrijfsnetwerk, in de cloud Hallo en op apparaten, wordt een geweldige cloud-gebaseerde identiteit en toegang beheeroplossing noodzakelijk. Cloud-gebaseerde identiteiten zijn nu Hallo beste manier toomaintain besturingselement over en inzicht in hoe en wanneer gebruikers toegang krijgen tot zakelijke toepassingen en gegevens.

Microsoft heeft identiteiten voor een cloud-gebaseerde is beveiligen via een tien jaar en nu met [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), deze dezelfde beveiliging-systemen tooyou beschikbaar zijn. Met Azure AD zorg Ondernemingsadministrators eenvoudig gebruiker en de beheerder accountability met betere beveiliging en beheeracties dan ooit tevoren.

Azure AD Premium is een cloud-gebaseerde identiteit en toegang beheeroplossing met geavanceerde beveiliging mogelijkheden waarmee een beveiligde identiteit voor alle apps, identity protection (verbeterd door Hallo [intelligence beveiliging voor Microsoft graph](https://www.microsoft.com/en-us/security/intelligence)), en Privileged Identity Management. Niet gewoon een bewaking of rapportage, Azure AD Premium kan uw gebruikersidentiteiten in realtime te beveiligen en het inschakelen van u toocreate risico, adaptieve toegang beleid tooprotect gegevens van uw organisatie.

Bekijk deze korte video voor een snel overzicht van Azure AD identity management en beveiliging:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft biedt niet alleen een identiteit waarmee u overal gaat, maar ook een set hulpprogramma's voor tooautomate, helpen beveiligen en beheren IT binnen uw organisatie. Zelfs na het Hallo-komst van cloudcomputing er nog steeds toomanage vraag en IT-taken beheren zoals helpdesk tooreset wachtwoorden van gebruikers roept, gebruikersgroep beheer en aanvragen van toepassingen. Complicerende dingen verdere, zijn werknemers nu de toowork van hun eigen apparaten meebrengen en direct beschikbaar SaaS-toepassingen. Hierdoor kunt u beheren van controle over hun toepassingen verschillende bedrijfsdatacenters en openbare cloudplatforms een belangrijke uitdaging.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Verbinding maken met on-premises Active Directory met Azure AD en Office 365
Organisaties die grote investeringen hebt gedaan in de lokale Active Directory kunnen u deze investeringen toohello cloud uitbreiden door hun on-premises adreslijsten integreren met Azure AD in [beheer van hybride identiteit](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). In dat geval, worden uw gebruikers productiever omdat zij één identiteit hebben voor toegang tot resources, ongeacht de locatie. Gebruikers en organisaties kunnen vervolgens worden gebruikt voor eenmalige aanmelding (SSO) tooaccess zowel lokale bronnen en cloudservices zoals Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) Hallo enige hulpprogramma u tooget Hallo integratie gedaan nodig is. Azure AD Connect biedt mogelijkheden toosupport uw identiteitssynchronisatie moet en vervangt oudere versies van identiteitsintegratie zoals DirSync en Azure AD Sync. Met Azure AD Connect wordt voor identiteits- en de synchronisatie tussen on-premises en Azure AD ingeschakeld via:

- Synchronisatie : met dit onderdeel worden gebruikers, groepen en andere objecten aangemaakt. Het is ook om te controleren of Hallo cloud komt overeen met de gegevens van de identiteit voor uw on-premises gebruikers en groepen. Terugschrijven van wachtwoord kan ook worden ingeschakeld tookeep on-premises adreslijsten synchroon worden wanneer een gebruiker het wachtwoord in Azure AD-updates.
- AD FS - federatie is een optionele functionaliteit verstrekt door Azure AD Connect die gebruikt tooconfigure een hybride omgeving met een worden kan on-premises AD FS-infrastructuur. Federation kan worden gebruikt door organisaties tooaddress complexe implementaties, zoals het eenmalige aanmelding, afdwinging van AD-aanmelden-beleid, en smartcard of een derde partij MFA.
- Statusbewaking - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) kan goede bewaking en een centrale locatie in Azure portal tooview Hallo bieden deze activiteit.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Productiviteit verhogen, en verlagen de kosten van de helpdesk met zelf en eenmalige aanmelding

Werknemers kunnen productiever wanneer ze een enkele tooremember gebruikersnaam en wachtwoord en een consistente ervaring vanaf elk apparaat hebben. Ze ook tijd besparen wanneer ze kunnen uitvoeren selfservice taken, zoals [opnieuw instellen van een vergeten wachtwoord](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) of het aanvragen van toegang tooan toepassing zonder te wachten op voor hulp bij Hallo helpdesk.

Azure AD [op de lokale Active Directory breidt](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) inschakelen in de cloud hello, toouse gebruikers hun primaire organisatieaccount voor zowel hun apparaten domein bedrijfsbronnen en alle Hallo web en SaaS-toepassingen ze moet toouse tooget hun werk. Bovendien toonot tooremember meerdere sets van gebruikersnamen en wachtwoorden, toegang tot gebruikers toepassingen kunnen ook worden automatisch ingericht (of buiten gebruik gesteld) met gebaseerd op hun groepslidmaatschappen van de organisatie en hun status als een werknemer. En u kunt beheren die toegang voor galerie apps of voor uw eigen lokale apps die u hebt ontwikkeld en gepubliceerd via Hallo [Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Beheren en toegang tot toocorporate bronnen bepalen
Microsoft identiteits- en toegangsbeheer management oplossingen zorgen ervoor dat IT beveiligen toegang tooapplications en bronnen in zakelijke datacenter hello en in de cloud hello, zoals het inschakelen van extra niveaus van de validatie van [multi-factorauthenticatie](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) en [beleidsregels voor voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Bewaking verdachte activiteiten via geavanceerde beveiliging rapportage, controle en waarschuwingen helpt bij het verminderen mogelijke beveiligingsproblemen.

Beleid voor voorwaardelijke toegang in Azure AD Premium kunnen u, Hallo ondernemingsadministrator, Hallo mogelijkheid toocreate op basis van beleid toegangsregels voor elke Azure AD verbonden-toepassing (SaaS-apps, aangepaste apps die worden uitgevoerd in Hallo cloud of on-premises webtoepassingen). Azure AD evalueert deze beleidsregels in realtime en dwingt deze telkens wanneer een gebruiker tooaccess probeert een toepassing. Azure identity protection-beleid kunnen u de actie ondernemen tooautomatically als verdachte activiteit wordt gedetecteerd. Deze acties kunnen bevatten toegang toousers op een hoog risico, afdwingen van multi-factor authentication-server, worden geblokkeerd en gebruikerswachtwoorden opnieuw instellen als het lijkt erop dat de referenties zijn aangetast.


## <a name="azure-active-directory-privileged-identity-management"></a>Privileged Identity Management voor Azure Active Directory

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), die deel uitmaakt van Azure Active Directory Premium P2 Hallo oplossing, kunt u toodiscover, Beperk en bewaak beheerdersaccounts en hun tooresources toegang in uw Azure Active Directory en andere Microsoft online services. Ook kunt u de beheerderstoegang op aanvraag voor Hallo exacte tijd hoeft te beheren.

Privileged Identity Management kunt beheerdersrechten op aanvraag afdwingen, zodat beheerders kunnen meerdere factoren geverifieerde, tijdelijke verhoging van hun bevoegdheden voor vooraf geconfigureerde perioden voordat hun accounts tooa normale aanvragen de status van de gebruiker.

## <a name="benefits-of-azure-identity"></a>Voordelen van Azure identiteit

Met Azure identity management kunt u:

-   Maken en beheren voor elke gebruiker één identiteit voor uw hele onderneming opzetten, gegevens synchroniseren gebruikers, groepen en apparaten met [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Eenmalige aanmelding toegang bieden tooyour toepassingen, waaronder duizenden vooraf geïntegreerde SaaS-apps of geef veilige externe toegang tooon-premises SaaS-toepassingen met Hallo [Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Toepassingsbeveiliging toegang inschakelen door af te dwingen op basis van regels [multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) voor zowel on-premises en cloud toepassingen.

-   De gebruikersproductiviteit met [selfservice voor wachtwoordherstel](https://docs.microsoft.com/azure/active-directory/active-directory-passwords), en de groep en de toepassing toegang aanvragen via Hallo [MyApps portal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Profiteren van Hallo [hoge beschikbaarheid en betrouwbaarheid](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) van een wereldwijd bedrijfsniveau cloud-gebaseerde identiteit en toegang beheeroplossing.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Azure-identiteitsoplossingen](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)