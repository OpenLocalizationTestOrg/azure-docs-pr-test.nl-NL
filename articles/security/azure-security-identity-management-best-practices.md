---
title: aaaAzure identity & access aanbevolen beveiligingsprocedures | Microsoft Docs
description: In dit artikel biedt een set met aanbevolen procedures voor het identiteitsbeheer en toegang beheren met ingebouwde mogelijkheden van Azure.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Azure voor identiteits- en toegang beheren best practices voor beveiliging
Veel Overweeg toobe Hallo nieuwe grens identiteitlaag voor beveiliging die rol vanuit Hallo traditioneel netwerk gericht perspectief overneemt. Deze evolutie van primaire pivot Hallo voor aandacht voor beveiliging en investeringen afkomstig zijn van Hallo feit dat netwerkverbindingen steeds poreuze geworden en mag geen die perimeternetwerk zo effectief als ze eenmaal voorafgaande toohello explosie van waren[BYOD](http://aka.ms/byodcg) apparaten en cloud-toepassingen.

In dit artikel wordt een verzameling Azure identiteits- en aanbevolen beveiligingsprocedures access control besproken. Deze aanbevolen procedures zijn afgeleid van onze ervaring met [Azure AD](../active-directory/active-directory-whatis.md) en Hallo ervaringen van klanten, zoals zelf.

Voor elke aanbevolen procedure wordt uitgelegd:

* Welke beste Hallo
* Waarom u wilt dat tooenable die best practices
* Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
* Mogelijke alternatieven toohello best practices
* Hoe meer u tooenable Hallo best practices

Deze Azure identiteitsbeheer en toegang beheren van beveiliging best practices artikel is gebaseerd op een advies consensus en mogelijkheden van Azure-platform en functiesets, als deze bestaan in Hallo tijd die in dit artikel is geschreven. Adviezen en technologieën op den duur veranderen en dit artikel worden de wijzigingen op een tooreflect regelmatig wordt bijgewerkt.

Azure identity management en toegang besturingselement aanbevolen beveiligingsprocedures besproken in dit artikel zijn onder andere:

* Uw identiteitsbeheer centraliseren
* Eenmalige aanmelding (SSO) inschakelen
* Wachtwoordbeheer implementeren
* Afdwingen van multi-factor authentication (MFA) voor gebruikers
* Gebruik rollen gebaseerd toegangsbeheer (RBAC)
* Locaties waar resources worden gemaakt met resourcemanager beheren
* Handleiding voor ontwikkelaars tooleverage identiteitsmogelijkheden voor SaaS-apps
* Actief bewaken voor verdachte activiteiten

## <a name="centralize-your-identity-management"></a>Uw identiteitsbeheer centraliseren
Een belangrijke stap voor het beveiligen van uw identiteit tooensure is dat deze accounts kan beheren vanaf één enkele locatie met betrekking tot waarop dit account is gemaakt. Tijdens het Hallo meerderheid van de Hallo ondernemingen IT-organisaties hebben hun primaire account directory on-premises en hybride cloud-implementaties zijn op Hallo aanleiding is het belangrijk dat u begrijpt hoe toointegrate lokale en cloudadreslijsten en bieden een naadloze ervaring toohello eindgebruiker.

tooaccomplish dit [hybride identiteit](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) scenario raadzaam twee opties:

* Uw on-premises directory worden gesynchroniseerd met uw clouddirectory via Azure AD Connect
* Uw on-premises identiteits met uw cloud directory met federeren [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)

Organisaties die niet voldoen aan toointegrate met hun on-premises identiteits met hun cloudidentiteit krijgen verhoogde administratieve overhead bij het beheren van accounts die verhoogt de kans op Hallo van fouten en beveiligingsrisico's.

Lees voor meer informatie over Azure AD-synchronisatie Hallo artikel [uw on-premises identiteiten integreren met Azure Active Directory](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Eenmalige aanmelding (SSO) inschakelen
Wanneer u meerdere mappen toomanage hebt, dit wordt een administratieve probleem niet alleen voor IT, maar ook voor eindgebruikers die tooremember meerdere wachtwoorden hebben. Met behulp van [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) u kunnen uw gebruikers Hallo Hallo gebruik dezelfde set referenties toosign in en open Hallo-resources die ze nodig hebben, ongeacht waar deze resource zich lokaal is of in Hallo cloud.

Gebruik van eenmalige aanmelding tooenable gebruikers tooaccess hun [SaaS-toepassingen](../active-directory/active-directory-appssoaccess-whatis.md) op basis van hun organisatieaccount in Azure AD. Dit geldt niet alleen voor Microsoft SaaS-apps, maar ook met andere apps, zoals [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) en [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). Uw toepassing kan worden geconfigureerd toouse Azure AD als een [SAML gebaseerde identiteit](../active-directory/fundamentals-identity.md) provider. Als een beveiligingscontrole geeft Azure AD geen token van een zodat ze toosign in toepassing hello tenzij ze gebruikmaken van Azure AD toegang hebben gekregen. U kunt toegang verlenen rechtstreeks of via een groep dat ze lid van zijn.

> [!NOTE]
> Hallo besluit toouse SSO invloed op hoe u uw on-premises directory integreren met uw clouddirectory. Als u wilt dat eenmalige aanmelding, moet u toouse Federatie, omdat adreslijstsynchronisatie alleen leveren [dezelfde ervaring voor eenmalige aanmelding](../active-directory/active-directory-aadconnect.md).
>
>

Organisaties die eenmalige aanmelding niet voor hun gebruikers en toepassingen afdwingen zijn meer blootgestelde tooscenarios waar gebruikers meerdere wachtwoorden die rechtstreeks verhoogt de kans op Hallo van gebruikers hergebruik van wachtwoorden of met behulp van zwakke wachtwoorden hebben.

U meer informatie over Azure AD SSO door te lezen Hallo artikel [AD FS-beheer en aanpassingen met Azure AD Connect](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Wachtwoordbeheer implementeren
In scenario's waarbij u meerdere tenants of u wilt dat gebruikers van tooenable te[hun eigen wachtwoord opnieuw instellen](../active-directory/active-directory-passwords-update-your-own-password.md), is het belangrijk dat u het juiste beleid tooprevent misbruik. U kunt in Azure Hallo zelf uw wachtwoord opnieuw instellen van mogelijkheid benutten en aanpassen Hallo beveiliging opties toomeet uw zakelijke vereisten.

Het is vooral belangrijk tooobtain feedback van gebruikers en meer uit hun ervaringen als ze proberen tooperform deze stappen. Op basis van deze ervaring, een plan toomitigate potentiële problemen die optreden tijdens het Hallo-implementatie voor een grotere groep lichten. Het is ook raadzaam dat u Hallo [activiteit voor wachtwoord opnieuw instellen registratie rapport](../active-directory/active-directory-passwords-get-insights.md) toomonitor Hallo gebruikers die zijn geregistreerd.

Organisaties die tooavoid wachtwoord willen wijzigen ondersteuningsoproepen maar schakel tooreset gebruikers hun eigen wachtwoorden vatbaarder tooa hogere aanroep volume toohello servicedesk vanwege toopassword problemen zijn. In organisaties die meerdere tenants hebben, is het noodzakelijk dat u dit type mogelijkheid implementeren en gebruikers tooperform wachtwoordherstel binnen de beveiligingsgrenzen van de die zijn vastgelegd in het beveiligingsbeleid Hallo inschakelen.

U kunt meer informatie over wachtwoord opnieuw instellen door te lezen Hallo artikel [wachtwoordbeheer implementeren en training gebruikers toouse het](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Afdwingen van multi-factor authentication (MFA) voor gebruikers
Voor organisaties die toobe compatibel zijn met de industriestandaarden, zoals [PCI DSS versie 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), multi-factor authentication-server is een moet hebben de mogelijkheid voor het verifiëren van gebruikers. Afgezien van dat compatibel is met de industriestandaarden, afdwingen van MFA tooauthenticate gebruikers kan ook helpen organisaties toomitigate credential theft type aanval, zoals [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).

Als u Azure MFA inschakelt voor uw gebruikers, voegt u een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties. In dit geval een transactie kan toegang krijgen tot een document dat zich in een bestandsserver of op uw SharePoint Online. Azure MFA helpt ook bij IT tooreduce Hallo kans op een verdachte referenties heeft toegang tot tooorganization van gegevens.

Bijvoorbeeld: u Azure MFA afdwingen voor uw gebruikers en configureert toouse een telefoongesprek of SMS-bericht naar deze verificatie. Als de referenties van gebruiker Hallo verdacht zijn, niet het Hallo aanvaller geval kunnen tooaccess worden alle bronnen omdat hij geen toegang tot toouser van telefoon. Organisaties die Voeg geen extra beveiligingslagen identiteit zijn vatbaar voor referentie diefstal aanval, wat toodata inbreuk leiden kan.

Een alternatief voor organisaties die tookeep Hallo gehele verificatiemethoden willen lokale is toouse [Azure multi-factor Authentication-Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), ook wel MFA lokale. Met deze methode wordt u nog steeds kunnen tooenforce multi-factor authentication-server, terwijl de Hallo MFA server on-premises, zijn.

Lees voor meer informatie over Azure MFA Hallo artikel [aan de slag met Azure multi-factor Authentication in de cloud Hallo](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Gebruik rollen gebaseerd toegangsbeheer (RBAC)
De toegang beperken op basis van Hallo [moet tooknow](https://en.wikipedia.org/wiki/Need_to_know) en [minimale bevoegdheden](https://en.wikipedia.org/wiki/Principle_of_least_privilege) beveiligingsprincipes is van cruciaal belang voor organisaties die tooenforce beveiligingsbeleid voor toegang tot gegevens willen. Azure op rollen gebaseerde toegangsbeheer (RBAC) kan worden gebruikt tooassign machtigingen toousers, groepen en toepassingen op een bepaalde scope. Hallo-bereik van een roltoewijzing kan dit een abonnement, een resourcegroep of één resource.

U kunt gebruikmaken van [ingebouwde RBAC](../active-directory/role-based-access-built-in-roles.md) rollen in Azure tooassign bevoegdheden toousers. Overweeg het gebruik van *Storage Account Inzender* voor cloudoperators die toomanage storage-accounts nodig en *klassieke Storage Account Inzender* rol toomanage klassieke opslagaccounts. Voor cloudoperators die behoeften toomanage VM's en storage-account, kunt u deze toe te voegen te*Virtual Machine Contributor* rol.

Organisaties die niet afgedwongen door toegangsbeheer gegevens dankzij het gebruik van mogelijkheden, zoals RBAC mogelijk meer bevoegdheden beschikt dan noodzakelijk tootheir gebruikers geven. Dit kan ertoe leiden dat toodata inbreuk door zodat gebruikers toegang hebben toocertain typen soorten gegevens (bijvoorbeeld invloedrijk) die de eerste plaats Hallo mag niet nodig hebben.

U kunt meer informatie over Azure RBAC Hallo artikel lezen [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Locaties waar resources worden gemaakt met resourcemanager beheren
Inschakelen van cloud-operators tooperform taken terwijl toomanage zo wordt voorkomen dat ze op te splitsen conventies die zijn vereist bronnen van uw organisatie is erg belangrijk. Organisaties die willen toocontrol Hallo locaties waar resources zijn gemaakt moeten harde code voor deze locaties.

tooachieve deze organisaties kunnen maken van beleidsregels voor veiligheid zijn gedefinieerd die worden beschreven Hallo acties of bronnen die specifiek worden geweigerd. U toewijzen deze beleidsdefinities op Hallo gewenst bereik, zoals Hallo abonnement, resourcegroep of een afzonderlijke resource.

> [!NOTE]
> Dit is dezelfde niet Hallo als RBAC, het daadwerkelijk maakt gebruik van RBAC tooauthenticate Hallo gebruikers die bevoegdheid toocreate die bronnen hebben.
>
>

Hefboomwerking [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toocreate aangepaste beleidsregels voor scenario's waarbij Hallo organisatie wil tooallow operations alleen wanneer Hallo juiste kostenplaats is ook gekoppeld; anders ze Hallo-aanvraag wordt geweigerd.

Organisaties die niet zijn beheren hoe resources worden gemaakt zijn vatbaarder toousers die misbruik Hallo service maken mogelijk door het maken van meer bronnen dan ze nodig hebben. Hallo-proces voor het maken van resource beperking is een belangrijke stap toosecure een scenario met meerdere tenants.

U kunt meer informatie over het maken van beleid met Azure Resource Manager door te lezen Hallo artikel [beleid toomanage resources en toegang beheren](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Handleiding voor ontwikkelaars tooleverage identiteitsmogelijkheden voor SaaS-apps
Gebruikersidentiteit zal worden gebruikt in veel scenario's als gebruikers toegang hebben tot [SaaS-apps](https://azure.microsoft.com/marketplace/active-directory/all/) die kunnen worden geïntegreerd met on-premises of clouddirectory. Allereerst omdat aangeraden ontwikkelaars gebruiken een beveiligde methodologie toodevelop deze apps zoals [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx). Azure AD authentication vereenvoudigt voor ontwikkelaars dankzij de identiteit als een service met ondersteuning voor industriestandaard-protocollen, zoals [OAuth 2.0](http://oauth.net/2/) en [OpenID Connect](http://openid.net/connect/), evenals de open-source bibliotheken voor verschillende platforms.

Zorg ervoor dat tooregister alle toepassingen die verificatie tooAzure AD heeft, is dit een verplichte procedure. Hallo komt achter dit omdat Azure AD toocoordinate Hallo communiceren met de Hallo toepassing moet bij het verwerken van eenmalige aanmelding (SSO) of uitwisselen van tokens. Hallo gebruikerssessie verloopt wanneer Hallo levensduur van Hallo token dat is uitgegeven door Azure AD is verlopen. Altijd geëvalueerd als uw toepassing deze tijd gebruikt of als u kunt deze tijd verkorten. Verminderen Hallo levensduur kan fungeren als veiligheidsmaatregel die gebruikers toosign uit op basis van een periode van inactiviteit forceert.

Organisaties die identiteit besturingselement tooaccess apps niet afdwingen en komen niet hun ontwikkelaars begeleiden op hoe toosecurely apps integreren met hun identiteitsbeheersysteem mogelijk vatbaarder toocredential diefstal type aanval, zoals [zwakke verificatie- en management beschreven in de toepassing van Open Web Project beveiliging (OWASP) Top 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

U meer informatie over verificatie scenario's voor SaaS-apps door te lezen [verificatie scenario's voor Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Actief bewaken voor verdachte activiteiten
Volgens het te[Verizon 2016 Data Breach rapport](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), referentiediefstal wordt nog steeds Hallo aanleiding en hoe een van de meest winstgevend bedrijven Hallo cyberbeveiliging criminelen. Daarom is het belangrijk toohave een actieve identiteit monitor beheersysteem die snel kunnen detecteren van de activiteit verdacht gedrag en activeren van een waarschuwing voor verder onderzoek. Azure AD heeft twee belangrijke mogelijkheden waarmee organisaties hun identiteit te controleren: Azure AD Premium [afwijkingsdetectie rapporten](../active-directory/active-directory-view-access-usage-reports.md) en Azure AD [identity protection](../active-directory/active-directory-identityprotection.md) mogelijkheid.

Zorg ervoor dat toouse hello afwijkingsdetectie rapporten tooidentify pogingen toosign in [zonder wordt getraceerd](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [beveiligingsaanvallen](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) aanmelden voor aanvallen op een bepaald account pogingen toosign in vanaf meerdere locaties van [geïnfecteerde apparaten](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) en verdachte IP-adressen. Houd er rekening mee dat deze rapporten. U moet met andere woorden, processen en procedures in plaats voor IT-beheerders toorun deze rapporten op Hallo dagelijks uit te voeren of op aanvraag (gewoonlijk in een respons op incidenten scenario) hebben.

Daarentegen, Azure AD identity protection is een actieve controlesysteem en het Hallo huidige risico's op een eigen dashboard wordt gemarkeerd. Behalve dat ontvangt u ook dagelijkse samenvatting meldingen via e-mail. Het is raadzaam dat u Hallo risiconiveau volgens tooyour bedrijfsvereisten aanpassen. Hallo risiconiveau voor een risicogebeurtenis is een indicatie van Hallo ernst van Hallo risicogebeurtenis (hoog, Gemiddeld of laag). Hallo risiconiveau helpt Identity Protection gebruikers prioriteren Hallo acties ze tooreduce Hallo risico tootheir organisatie moeten nemen.

Organisaties die niet actief bewaak hun identiteitssystemen, lopen risico dat de referenties van de gebruiker is geknoeid. Plaats met deze referenties zonder medeweten die verdachte activiteiten zijn genomen, organisaties niet kunnen toomitigate dit type risico.
U meer informatie over Azure Identity protection door te lezen [Azure Active Directory: Identity Protection](../active-directory/active-directory-identityprotection.md).
