---
title: Active Directory bewijs van concept playbook bouwstenen aaaAzure | Microsoft Docs
description: Verkennen en snel implementeren scenario's voor Identity and Access Management
services: active-directory
keywords: Azure active directory, playbook, Proof-of-Concept, implementatiemodel
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory bewijs van concept playbook: bouwstenen

## <a name="catalog-of-roles"></a>Catalogus met rollen

| Rol | Beschrijving | Proof-of-concept (PoC) verantwoordelijkheid |
| --- | --- | --- |
| **Architectuur van de identiteit / ontwikkelteam** | Dit team is meestal Hallo een die Hallo oplossing ontwerpen, prototypen implementeert, goedkeuringen stations en tot slot draagt toooperations | Ze bieden Hallo-omgevingen en zijn Hallo die evaluatie Hallo verschillende scenario's vanuit Hallo beheerbaarheid perspectief |
| **On-Premises Identity operationele team** | Hallo andere identiteit bronnen lokale beheert: Active Directory-Forests, LDAP-adreslijsten, HR-systemen en federatieve id-Providers. | Bieden toegang tot tooon lokale bronnen die nodig zijn voor Hallo implementatiemodel scenario's.<br/>Ze moeten zo weinig mogelijk betrokken|
| **Technische Toepassingseigenaars** | Technische eigenaren van Hallo verschillende cloud-apps en services die is geïntegreerd met Azure AD | Gedetailleerde informatie bevat over SaaS-toepassingen (mogelijk exemplaren voor het testen) |
| **Globale beheerder van Azure AD** | Beheert de configuratie van hello Azure AD | Geef referenties op tooconfigure Hallo-synchronisatieservice. Meestal dezelfde team identiteit architectuur Hallo tijdens de POC-fase maar afzonderlijke tijdens Hallo operations fase|
| **Database-team** | Eigenaars van Hallo Database-infrastructuur | Het bieden van toegang tooSQL omgeving (AD FS of Azure AD Connect) voor specifieke scenario voorbereidingen.<br/>Ze moeten zo weinig mogelijk betrokken |
| **Netwerkteam** | Eigenaren van de netwerkinfrastructuur Hallo | Vereist toegang verlenen op netwerkniveau Hallo voor Hallo synchronisatie servers tooproperly toegang tot Hallo gegevensbronnen en cloud services-(firewall-regels, poorten die worden geopend, IPSec-regels, enz.) |
| **Beveiligingsteam** | Hallo beveiligingsstrategie definieert, analyseert beveiligingsrapporten uit diverse bronnen en volgt via op bevindingen. | Doel-beveiliging bieden evaluatie scenario 's |

## <a name="common-prerequisites-for-all-building-blocks"></a>Algemene vereisten voor alle bouwstenen

Hier volgen enkele vereisten die nodig zijn voor een Implementatiemodel met Azure AD Premium.

| Vereiste | Resources |
| --- | --- |
| Azure AD-tenant is gedefinieerd met een geldige Azure-abonnement | [Hoe tooget een Azure Active Directory-tenant](active-directory-howto-tenant.md)<br/>**Opmerking:** als u al een omgeving met Azure AD Premium-licenties hebt, kunt u een nul cap-abonnement downloaden door te navigeren toohttps://aka.ms/accessaad <br/>Meer informatie op: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ en https://technet.microsoft.com/library/dn832618.aspx |
| Domeinen gedefinieerd en geverifieerd | [Toevoegen van een aangepast domein naam tooAzure Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Opmerking:** sommige werkbelastingen, zoals Power BI kan hebt ingericht, een azure AD-tenant onder Hallo worden behandeld. toocheck als een bepaald domein is gekoppeld tooa-tenant, gaat u toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Als u een geslaagd antwoord, ophalen en vervolgens het Hallo-domein is al toegewezen aan tooa tenant en neemt mogelijk nodig. Als dit het geval is, moet u contact op met Microsoft voor verdere informatie. Meer informatie over Hallo overname opties op: [wat is Selfserviceregistratie voor Azure?](active-directory-self-service-signup.md) |
| Azure AD Premium of EMS-proefabonnement Enabled | [Azure Active Directory Premium voor één maand gratis](https://azure.microsoft.com/trial/get-started-active-directory/) |
| U hebt Azure AD Premium of EMS-licenties toegewezen tooPoC gebruikers | [Licentie uzelf en uw gebruikers in Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Azure globale beheerder van AD-referenties | [Beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Optioneel maar ten zeerste aanbevolen: parallelle testomgeving als terugval | [Vereisten voor Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Nieuwe installatie van Directory - Wachtwoordhashsynchronisatie (PBS) - synchronisatie

Geschatte tijd tooComplete: één uur voor minder dan 1000 gebruikers van de POC-fase

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Server tooRun Azure AD Connect | [Vereisten voor Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Doelgroep is gebruikers van de POC-fase, in Hallo hetzelfde domein en deel uitmaken van een beveiligingsgroep en organisatie-eenheid | [Aangepaste installatie van Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD Connect-functies die nodig zijn voor Hallo Implementatiemodel worden geïdentificeerd | [Verbinding maken met Active Directory met Azure Active Directory - synchronisatie instellen functies](./connect/active-directory-aadconnect.md#configure-sync-features) |
| U hebt referenties nodig voor on-premises en in de cloud omgevingen  | [Azure AD Connect: accounts en machtigingen](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Hallo meest recente versie van Azure AD Connect downloaden | [Microsoft Azure Active Directory Connect downloaden](https://www.microsoft.com/download/details.aspx?id=47594) |
| Azure AD Connect installeren met het eenvoudigste Hallo-pad: Express <br/>1. Toohello organisatie-eenheid toominimize Hallo Synchronisatiecyclus doeltijd filteren<br/>2. Kies doel groep gebruikers in de Hallo lokale groep.<br/>3. Hallo-functies die nodig is door Hallo andere Implementatiemodel thema's implementeren | [Azure AD Connect: Aangepaste installatie: domein en OE filteren](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Aangepaste installatie: groep gebaseerd filteren](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Uw on-premises identiteiten integreren met Azure Active Directory: synchronisatie-functies configureren](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Hello Azure AD Connect UI openen en bekijken met Hallo profielen voltooide is (Import, synchronisatie en uitvoer) | [Azure AD Connect sync: Scheduler](./connect/active-directory-aadconnectsync-feature-scheduler.md) (Azure AD Connect-synchronisatie: planning) |
| Open Hallo [Azure AD-beheerportal](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), gaat u toohello 'Alle gebruikers' blade, toevoegen 'Bron van de autorisaties' kolom en om te zien die Hallo gebruikers worden weergegeven, correct worden gemarkeerd als het afkomstig is van 'WindowsServer AD' | [Azure AD-beheerportal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Overwegingen

1. Bekijkt hello beveiligingsoverwegingen voor wachtwoordhashsynchronisatie [hier](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Als wachtwoordhashsynchronisatie voor productiegebruikers definitief niet optioneel is, kunt u Hallo alternatieven te volgen:
   * Testgebruikers maken in het productiedomein Hallo. Zorg ervoor dat u een andere account niet synchroniseren
   * Tooan UAT omgeving verplaatsen
2.  Als u toopursue federation wilt, is het nuttig toounderstand Hallo de kosten voor een federatieve oplossing lokale id-Provider buiten Hallo Implementatiemodel en die tegen Hallo voordelen biedt voor u op zoek bent naar:
    * Het is in kritieke pad Hallo zodat u toodesign voor hoge beschikbaarheid hebt
    * Het is een lokale service moet u toocapacity plannen
    * Het is een lokale service moet u toomonitor, onderhouden/patch

Meer informatie: [identiteit Understanding Office 365 en Azure Active Directory - federatieve identiteit](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>De huisstijl

Geschatte tijd tooComplete: 15 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Activa (afbeeldingen, logo's, enzovoort); Zorg ervoor Hallo activa hebben Hallo aanbevolen grootten voor best visualisatie. | [Huisstijl tooyour aanmeldingspagina in hello Azure Active Directory toevoegen](active-directory-branding-custom-signon-azure-portal.md) |
| Optioneel: Als Hallo-omgeving heeft de ADFS-server, toegang tot toohello server toocustomize webthema | [AD FS-gebruiker aanmelden aanpassing](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Client computer tooperform eindgebruikerservaring-aanmelding |  |
| Optioneel: Mobiele apparaten toovalidate ervaring |  |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Ga tooAzure AD-beheerportal | [Azure AD-beheerportal - huisstijl van uw bedrijf](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Upload Hallo activa voor Hallo-aanmeldingspagina (hero logo, kleine logo, labels, enzovoort). Optioneel als u AD FS hebt, uitlijnen Hallo dezelfde activa met AD FS-aanmeldingspagina's | [Huisstijl tooyour aanmelden en Toegangsvenster toevoegen: aanpasbare elementen](active-directory-add-company-branding.md) |
| Wacht een paar minuten voor Hallo wijziging toofully wordt pas van kracht |  |
| Aanmelden met Hallo Implementatiemodel gebruiker referentie toohttps://myapps.microsoft.com |  |
| Hallo uiterlijk in browser bevestigen | [Huisstijl tooyour aanmelden en Toegangsvenster toevoegen](active-directory-add-company-branding.md) |
| Eventueel Hallo uiterlijk in andere apparaten bevestigen |  |

### <a name="considerations"></a>Overwegingen

Als het oude uiterlijk Hallo blijft na het aanpassen van Hallo Hallo browser clientcache leegmaken en probeer opnieuw Hallo.

## <a name="group-based-licensing"></a>Groeperen op basis van de licentieverlening

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Alle gebruikers van de POC-fase uitmaken deel van een beveiligingsgroep (cloud of on-premises) | [Een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Ga toolicenses blade in Azure AD-beheerportal | [Azure AD-beheerportal: licentieverlening](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Hallo licenties toohello beveiligingsgroep met Implementatiemodel gebruikers toewijzen. | [Toewijzen van licenties tooa groep gebruikers in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Overwegingen

In geval van problemen, ga te[scenario's, beperkingen en bekende problemen met het gebruik van groepen toomanage licentieverlening in Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Configuratie van de SaaS-federatieve SSO

Geschatte tijd tooComplete: 60 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| De testomgeving Hallo SaaS-toepassing. In deze handleiding gebruiken we ServiceNow als voorbeeld.<br/>Wij raden toouse een test exemplaar toominimize wrijving op de kwaliteit van de bestaande gegevens en toewijzingen te navigeren. | Ga toohttps://developer.servicenow.com/app.do#! / home toostart Hallo proces van het ophalen van een exemplaar van de test |
| Beheerder toegang toohello ServiceNow-beheerconsole | [Zelfstudie: Azure Active Directory-integratie met ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Het doel ingesteld van de gebruikers tooassign Hallo toepassing. Een beveiligingsgroep met Hallo implementatiemodel gebruikers wordt aanbevolen. <br/>Als maken Hallo-groep niet haalbaar is, Hallo gebruikers toewijzen toodirectly toohello-toepassing voor Hallo implementatiemodel | [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Hallo zelfstudie tooall actoren van Microsoft Documentation delen  | [Zelfstudie: Azure Active Directory-integratie met ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Stelt een vergadering werken en stappen Hallo zelfstudie met elke acteur. | [Zelfstudie: Azure Active Directory-integratie met ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Toewijst Hallo app toohello in Hallo vereisten geïdentificeerd. Als Hallo Implementatiemodel voorwaardelijke toegang in het Hallo-bereik heeft, kunt u dat later terugkeren naar en toevoegen van MFA en vergelijkbare. <br/>Houd er rekening mee dat wordt dit kick in Hallo inrichtingsproces (indien geconfigureerd) |  [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Azure AD management Portal tooadd ServiceNow-toepassing uit de galerie gebruiken| [Azure AD management Portal: bedrijfstoepassingen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| "Eenmalige aanmelding' Blade van ServiceNow-App ' op basis van SAML-aanmelding inschakelen" |  |
| Vul 'Aanmelding op URL' en 'Id' velden aan uw ServiceNow-URL<br/>Hallo selectievakje te 'nieuw certificaat actief maken'<br/>en instellingen op te slaan |  |
| Open 'ServiceNow configureren' blade op Hallo Hallo Configuratiescherm tooview onderaan aangepaste instructies voor het tooconfigure ServiceNow |  |
| Volg de instructies tooconfigure ServiceNow |  |
| Op de blade 'Inrichten' van ServiceNow App 'Automatisch' inrichting inschakelen | [Het beheer van gebruikersaccount inrichten voor zakelijke apps in Hallo nieuwe Azure-portal](active-directory-enterprise-apps-manage-provisioning.md) |
| Wacht een paar minuten tijdens het inrichten is voltooid.  In Hallo tussentijd kunt u controleren op Hallo inrichting rapporten |  |
| Meld u bij toohttps://myapps.microsoft.com/ als een testgebruiker die toegang heeft | [Wat is Hallo Toegangsvenster?](active-directory-saas-access-panel-introduction.md) |
| Klik op de tegel Hallo voor Hallo-toepassing die is gemaakt. Toegang bevestigen |  |
| U kunt eventueel Hallo toepassing gebruiksrapporten controleren. Houd er rekening mee dat er is enige vertraging worden bijgewerkt, dus moet u toowait tijd toosee Hallo verkeer in Hallo-rapporten. | [Aanmeldingsactiviteiten rapporten in Azure Active Directory-beheerportal Hallo: informatie over het gebruik van beheerde toepassingen](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Retentiebeleid voor Azure Active Directory-rapporten) |

### <a name="considerations"></a>Overwegingen

1. Hierboven [zelfstudie](active-directory-saas-servicenow-tutorial.md) tooold Azure AD-beheerervaring verwijst. Maar implementatiemodel is gebaseerd op [snel starten](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away) optreden.
2. Als het Hallo-doeltoepassing is niet aanwezig in de galerie hello, kunt klikt u vervolgens u 'Bring your own app'. Meer informatie: [wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: het toevoegen van aangepaste toepassingen vanaf één locatie](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>SaaS-wachtwoord SSO-configuratie

Geschatte tijd tooComplete: 15 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| De testomgeving voor SaaS-toepassingen. Een voorbeeld van een wachtwoord SSO is HipChat en Twitter. Voor een andere toepassing moet u de exacte URL Hallo van Hallo-pagina met HTML-aanmeldingspagina formulier. | [Twitter op Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat op Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Testaccounts voor Hallo-toepassingen. | [Aanmelden voor Twitter](https://twitter.com/signup?lang=en)<br/>[Aanmelden voor gratis: HipChat](https://www.hipchat.com/sign_up) |
| Het doel ingesteld van de gebruikers tooassign Hallo toepassing. Een opgenomen Hallo beveiligingsgroepgebruikers wordt aanbevolen. | [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Lokale beheerder toegang tooa computer toodeploy Hallo Configuratiescherm-uitbreiding voor toegang voor Internet Explorer, Chrome of Firefox | [Configuratiescherm-extensie voor IE toegang](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Uitbreiding van het Configuratiescherm toegang voor Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Uitbreiding van het Configuratiescherm toegang voor Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Hallo Browseruitbreiding installeren | [Configuratiescherm-extensie voor IE toegang](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Uitbreiding van het Configuratiescherm toegang voor Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Uitbreiding van het Configuratiescherm toegang voor Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Toepassing vanuit galerie configureren | [Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: Hallo nieuwe en verbeterde toepassingsgalerie](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Wachtwoord eenmalige aanmelding configureren | [Het beheren van eenmalige aanmelding voor zakelijke apps in de nieuwe Azure portal Hallo: Meld u op wachtwoord gebaseerde](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Hallo app toohello groep in Hallo vereisten geïdentificeerd toewijzen | [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Meld u bij toohttps://myapps.microsoft.com/ als een testgebruiker die toegang heeft |  |
| Klik op de tegel Hallo voor Hallo-toepassing die is gemaakt. | [Wat is er Hallo Toegangsvenster?: SSO zonder identiteit inrichten op basis van wachtwoorden](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Hallo toepassingsreferenties opgeven | [Wat is er Hallo Toegangsvenster?: SSO zonder identiteit inrichten op basis van wachtwoorden](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Hallo-browser en meld u aan herhaaldelijk Hallo sluiten. Hallo gebruiker ziet dit keer ongeveer naadloze toegang toohello toepassing. |  |
| U kunt eventueel Hallo toepassing gebruiksrapporten controleren. Houd er rekening mee dat er is enige vertraging worden bijgewerkt, dus moet u toowait tijd toosee Hallo verkeer in Hallo-rapporten. | [Aanmeldingsactiviteiten rapporten in Azure Active Directory-beheerportal Hallo: informatie over het gebruik van beheerde toepassingen](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Retentiebeleid voor Azure Active Directory-rapporten) |

### <a name="considerations"></a>Overwegingen

Als het Hallo-doeltoepassing is niet aanwezig in de galerie hello, kunt klikt u vervolgens u 'Bring your own app'. Meer informatie: [wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: het toevoegen van aangepaste toepassingen vanaf één locatie](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Houd er rekening mee Hallo volgens de vereisten:
   * Toepassing moet een bekende aanmeldings-URL
   * Hallo-aanmeldingspagina moet een HTML-formulier met een of meer tekstvelden die Hallo browseruitbreidingen kunnen automatisch invullen bevatten. Op Hallo minimale, moet gebruikersnaam en het wachtwoord bevatten.

## <a name="saas-shared-accounts-configuration"></a>SaaS gedeelde configuratie van Accounts

Geschatte tijd tooComplete: 30 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| lijst met doeltoepassingen Hallo en Hallo exacte aanmelden URL's tevoren. U kunt bijvoorbeeld Twitter. | [Twitter op Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Aanmelden voor Twitter](https://twitter.com/signup?lang=en) |
| Gedeelde referenties voor deze SaaS-toepassing. | [Delen van accounts met behulp van Azure AD](active-directory-sharing-accounts.md)<br/>[Azure AD geautomatiseerde wachtwoord roll gedurende Facebook, Twitter en LinkedIn nu in preview! -Enterprise Mobility and Security-Blog] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Referenties voor ten minste twee teamleden die toegang hebben tot hetzelfde account Hallo. Ze moet deel uitmaken van een beveiligingsgroep. | [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Lokale beheerder toegang tooa computer toodeploy Hallo Configuratiescherm-uitbreiding voor toegang voor Internet Explorer, Chrome of Firefox | [Configuratiescherm-extensie voor IE toegang](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Uitbreiding van het Configuratiescherm toegang voor Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Uitbreiding van het Configuratiescherm toegang voor Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Hallo Browseruitbreiding installeren | [Configuratiescherm-extensie voor IE toegang](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Uitbreiding van het Configuratiescherm toegang voor Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Uitbreiding van het Configuratiescherm toegang voor Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Toepassing vanuit galerie configureren | [Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: Hallo nieuwe en verbeterde toepassingsgalerie](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Wachtwoord eenmalige aanmelding configureren | [Het beheren van eenmalige aanmelding voor zakelijke apps in de nieuwe Azure portal Hallo: Meld u op wachtwoord gebaseerde](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Toewijst Hallo app toohello geïdentificeerd in Hallo vereisten bij het toewijzen van referenties | [Toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Meld u aan als verschillende gebruikers die app toegang als Hallo **dezelfde gedeelde account.**  |  |
| U kunt eventueel Hallo toepassing gebruiksrapporten controleren. Houd er rekening mee dat er is enige vertraging worden bijgewerkt, dus moet u toowait tijd toosee Hallo verkeer in Hallo-rapporten. | [Aanmeldingsactiviteiten rapporten in Azure Active Directory-beheerportal Hallo: informatie over het gebruik van beheerde toepassingen](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Retentiebeleid voor Azure Active Directory-rapporten) |


### <a name="considerations"></a>Overwegingen

Als het Hallo-doeltoepassing is niet aanwezig in de galerie hello, kunt klikt u vervolgens u 'Bring your own app'. Meer informatie: [wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: het toevoegen van aangepaste toepassingen vanaf één locatie](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Houd er rekening mee Hallo volgens de vereisten:
   * Toepassing moet een bekende aanmeldings-URL
   * Hallo-aanmeldingspagina moet een HTML-formulier met een of meer tekstvelden die Hallo browseruitbreidingen kunnen automatisch invullen bevatten. Op Hallo minimale, moet gebruikersnaam en het wachtwoord bevatten.

## <a name="app-proxy-configuration"></a>App-proxyconfiguratie

Geschatte tijd tooComplete: 20 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Een Microsoft Azure AD basic of premium-abonnement en een Azure AD-directory waarvoor u een globale beheerder bent | [Azure Active Directory-edities](active-directory-editions.md) |
| Een webtoepassing gehost on-premises dat u tooconfigure voor externe toegang wilt |  |
| Een server met Windows Server 2012 R2 of Windows 8.1 of hoger, waarop u Hallo Connector voor toepassingsproxy kunt installeren | [Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md) |
| Als er een firewall in Hallo pad, zorg ervoor dat deze geopend is zodat die Connector HTTPS (TCP) kunt maken Hallo toohello toepassingsproxy aanvragen | [Toepassingsproxy inschakelen in hello Azure-portal: vereisten voor toepassingsproxy](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Als uw organisatie gebruikmaakt van proxy servers tooconnect toohello internet, nemen bekijkt hello blog post werken met bestaande lokale proxyservers voor meer informatie over het tooconfigure ze | [Werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Een connector installeren op Hallo-server | [Toepassingsproxy inschakelen in hello Azure-portal: Installeer en registreer Hallo Connector](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Hallo on-premises toepassing publiceren in Azure AD als een toepassing toepassingsproxy | [Toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md) |
| Testgebruikers toewijzen | [Toepassingen publiceren met Azure AD-toepassingsproxy: een testgebruiker toevoegen](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Configureer desgewenst een ervaring voor eenmalige aanmelding voor uw gebruikers | [Geef eenmalige aanmelding met Azure AD-toepassingsproxy](application-proxy-sso-azure-portal.md) |
| Test-app aanmeldt tooMyApps-portal aan als gebruiker toegewezen | https://myapps.Microsoft.com |

### <a name="considerations"></a>Overwegingen

1. Terwijl het is raadzaam deze Hallo-connector in uw bedrijfsnetwerk, zijn er gevallen wanneer ziet u betere prestaties in de cloud Hallo plaatst. Meer informatie: [aandachtspunten voor topologie netwerk bij gebruik van Azure Active Directory-toepassingsproxy](application-proxy-network-topology-considerations.md)
2. Zie voor meer informatie over de beveiliging en hoe dit biedt een bijzonder veilige externe toegang oplossing door alleen uitgaande verbindingen onderhouden: [beveiligingsoverwegingen voor toegang tot de apps op afstand met behulp van Azure AD-toepassingsproxy](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Algemene configuratie van de LDAP-Connector

Geschatte tijd tooComplete: 60 minuten

> [!IMPORTANT]
> Dit is een geavanceerde configuratie vereisen enigszins bekend bent met FIM/MIM. Als het gebruikt in productie, wordt geadviseerd de vragen over deze configuratie gaat via [Premier Support](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Azure AD Connect geïnstalleerd en geconfigureerd | Bouwsteen: [adreslijstsynchronisatie - Wachtwoordhashsynchronisatie](#directory-synchronization--password-hash-sync-phs--new-installation) |
| ADLDS exemplaar vergadering vereisten | [Algemene LDAP-Connector, technische naslaginformatie: overzicht van Hallo algemene LDAP-Connector](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Lijst van werkbelastingen die van gebruikers gebruikmaken en kenmerken die zijn gekoppeld aan deze werkbelastingen | [Azure AD Connect-synchronisatie: kenmerken gesynchroniseerd tooAzure Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Algemene LDAP-Connector toevoegen | [Algemene LDAP-Connector, technische naslaginformatie: een nieuwe Connector maken](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Uitvoeringsprofielen maken voor gemaakte connector (volledige import, delta-import, volledige synchronisatie, Deltasynchronisatie, exporteren) | [Maken van een beheerprofiel van het uitvoeren van Agent](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Met behulp van connectors met hello Azure AD Connect Sync-Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Volledige import profiel uitvoeren en controleren, er zijn objecten in de connectorruimte | [Zoeken naar een Object van de ruimte Connector](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Met connectors Hello Azure AD Connect Sync-Service Manager: Connectorgebied zoeken](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Synchronisatieregels maakt, zodat objecten in de Metaverse over vereiste kenmerken voor werkbelastingen | [Azure AD Connect-synchronisatie: aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo: tooSynchronization regels wordt gewijzigd](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect-synchronisatie: inzicht declaratieve inrichting](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect-synchronisatie: inzicht declaratieve inrichting expressies](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Volledige synchronisatiecyclus starten | [Azure AD Connect-synchronisatie: Scheduler: Hallo scheduler starten](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| In geval van problemen wilt oplossen | [Een object dat niet tooAzure AD synchroniseert oplossen](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Controleer of, LDAP-gebruiker kunt aanmelden en toegang tot de toepassing hello | https://myapps.Microsoft.com |

### <a name="considerations"></a>Overwegingen

> [!IMPORTANT]
> Dit is een geavanceerde configuratie vereisen enigszins bekend bent met FIM/MIM. Als het gebruikt in productie, wordt geadviseerd de vragen over deze configuratie gaat via [Premier Support](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Groepen - overgedragen eigendom

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| SaaS-toepassing (federatieve SSO of wachtwoord SSO) is al geconfigureerd | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) |
| Cloud-groep die is toegewezen toegang toohello toepassing in #1 wordt geïdentificeerd. | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) <br/>[Een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Referenties voor de Groepseigenaar Hallo zijn beschikbaar | [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md) |
| Referenties voor Hallo information worker ze Hallo apps is geïdentificeerd | [Wat is Hallo Toegangsvenster?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Hallo-groep die is toegekend toegang toohello toepassing identificeren en configureer Hallo eigenaar van de opgegeven groep| [Hallo-instellingen voor een groep in Azure Active Directory beheren](active-directory-groups-settings-azure-portal.md) |
| Meld u aan als eigenaar van de groep Hallo, Zie Hallo groepslidmaatschap groepen tabblad van het toegangsvenster | [Azure Active Directory-groepen Management-pagina](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Hallo Informatiemedewerker u tootest wilt toevoegen |  |
| Meld u aan als Informatiemedewerker hello, bevestigen Hallo tegel beschikbaar is | [Wat is Hallo Toegangsvenster?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Overwegingen

Als de toepassing hello inrichting ingeschakeld heeft, moet u mogelijk toowait enkele minuten duren voor inrichting toocomplete voordat toegang tot de toepassing hello als Informatiemedewerker Hallo Hallo.

## <a name="saas-and-identity-lifecycle"></a>SaaS en Identity Lifecycle

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| SaaS-toepassing (federatieve SSO of wachtwoord SSO) is al geconfigureerd | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) |
| Cloud-groep die is toegewezen toegang toohello toepassing in #1 wordt geïdentificeerd. | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) <br/>[Een groep maken en leden toevoegen in Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Referenties voor Hallo information worker ze Hallo apps is geïdentificeerd | [Wat is Hallo Toegangsvenster?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Verwijder Hallo gebruiker uit Hallo groep Hallo app te is toegewezen| [Groepslidmaatschap voor gebruikers in uw Azure Active Directory-tenant beheren](active-directory-groups-members-azure-portal.md) |
| Wacht enkele minuten duren voordat de inrichting ongedaan | [Geautomatiseerde Gebruikersinrichting voor SaaS-App in Azure AD: hoe werkt geautomatiseerde inrichting?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Meld u aan als Hallo informatie worker toomy apps-portal en Bevestig dat tegel ontbreekt op een afzonderlijke browsersessie | http://myapps.Microsoft.com |


### <a name="considerations"></a>Overwegingen

Afleiden Hallo implementatiemodel scenario tooleavers en/of laat de eigenschap afwezig scenario's. Als de gebruiker Hallo opgehaald uitgeschakeld in on-premises AD dat of verwijderd, er niet langer een toolog manier in toohello SaaS-toepassing.

## <a name="self-service-access-tooapplication-management"></a>Self Servicetoegang tooApplication Management

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Implementatiemodel gebruikers die toegang toohello toepassingen, wordt gevraagd om u als onderdeel van de beveiligingsgroep Hallo identificeren | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) |
| Doeltoepassing geïmplementeerd | Bouwsteen: [SaaS federatieve SSO-configuratie](#saas-federated-sso-configuration) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Ga tooEnterprise toepassingen blade in Azure AD-beheerportal | [Azure AD-beheerportal: Bedrijfstoepassingen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| De toepassing van de vereisten met selfservice configureren | [Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory: toegang tot selfservice-toepassingen configureren](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Meld u aan als Hallo informatie worker toomy apps-portal | http://myapps.Microsoft.com |
| U ziet ' + app toevoegen ' knop op op Hallo pagina. Deze tooget toegang toohello app gebruiken |  |

### <a name="considerations"></a>Overwegingen

Hallo toepassingen gekozen hebben inrichting vereisten, zodat onmiddellijk toohello app gaat een aantal fouten kan veroorzaken. Als Hallo toepassing gekozen ondersteuning biedt voor inrichting met azure ad en deze is geconfigureerd, kunt u dit gebruiken als een kans tooshow Hallo hele stroom end tooend werkt. Zie Hallo bouwsteen voor [SaaS federatieve SSO configuratie](#saas-federated-sso-configuration) voor verdere aanbevelingen

## <a name="self-service-password-reset"></a>Selfservice voor wachtwoordherstel

Geschatte tijd tooComplete: 15 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Schakel het beheer van de selfservice voor wachtwoordherstel in uw tenant. | [Azure Active Directory-wachtwoord opnieuw instellen voor IT-beheerders](active-directory-passwords.md) |
| Wachtwoord terugschrijven toomanage wachtwoorden van on-premises inschakelen. Opmerking hiervoor specifieke Azure AD Connect-versies | [Vereisten voor het terugschrijven van wachtwoorden](active-directory-passwords-writeback.md) |
| Identificeer Hallo implementatiemodel gebruikers die deze functionaliteit gebruiken en zorg ervoor dat ze lid zijn van een beveiligingsgroep. Hallo-gebruikers moeten niet-beheerders toofully toepassingen Hallo mogelijkheid | [Aanpassen: Azure AD-wachtwoordbeheer: beperkte toegang toopassword opnieuw instellen](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Navigeer tooAzure AD-beheerportal: wachtwoord opnieuw instellen | [Azure AD-beheerportal: Wachtwoord opnieuw instellen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Bepaal Hallo wachtwoord opnieuw instellen van beleid. Voor de POC-doeleinden, kunt u telefonische oproep en Q & A. Het verdient aanbeveling tooenable registratie toobe vereist op aanmelden tooaccess Configuratiescherm |  |
| Meld u af en meld u aan als een Informatiemedewerker |  |
| Hallo selfservice voor wachtwoordherstel gegevens leveren, zoals geconfigureerd per stap 2 | http://aka.MS/ssprsetup |
| De browser sluiten Hallo |  |
| Hallo aanmeldingsproces beginnen als Hallo Informatiemedewerker die u in stap 4 gebruikt |  |
| Hallo-wachtwoord opnieuw instellen | [Uw eigen wachtwoord bijwerken: Mijn wachtwoord opnieuw instellen](active-directory-passwords-update-your-own-password.md) |
| Probeer aangemeld met uw nieuwe wachtwoord tooAzure AD evenals tooon lokale bronnen |  |

### <a name="considerations"></a>Overwegingen

1. Als upgraden hello Azure AD Connect toocause wrijving gaat, overwegen tegen accounts in de cloud of een demo tegen een afzonderlijke omgeving maken
2. Hallo-beheerders hebben een ander beleid en via Hallo beheerder accountwachtwoord tooreset Hallo mogelijk taint Hallo implementatiemodel en tot verwarring leiden. Zorg ervoor dat u een gewone gebruiker account tootest Hallo opnieuw instellen van bewerkingen gebruiken


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure multi-factor Authentication met telefoongesprekken

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Identificeer gebruikers Implementatiemodel met MFA  |  |
| Telefoon met goede ontvangst voor MFA uitdaging  | [Wat is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Navigeer te 'Gebruikers en groepen' blade in Azure AD-beheerportal | [Azure AD-beheerportal: Gebruikers en groepen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| 'Alle gebruikers' blade kiezen |  |
| In de bovenste Hallo balk de knop 'Multi-Factor Authentication' kiezen | Directe URL voor Azure MFA-portal: https://aka.ms/mfaportal |
| In de instellingen van Hallo 'Gebruiker' hello implementatiemodel gebruikers selecteren en deze voor MFA inschakelen | [Statuswaarden voor gebruikers in Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Meld u aan als Hallo implementatiemodel gebruiker en doorloop Hallo bewijs-up-proces  |  |

### <a name="considerations"></a>Overwegingen

1. Hallo implementatiemodel stappen in deze bouwsteen expliciet MFA instellen voor een gebruiker op alle aanmeldingen. Er zijn andere hulpprogramma's zoals voorwaardelijke toegang en Identity Protection MFA op meer benaderen gerichte scenario's. Dit is iets tooconsider bij het verplaatsen van de POC-fase tooproduction.
2. Hallo implementatiemodel stappen in deze bouwsteen telefoongesprekken expliciet als Hallo MFA-methode voor expedience gebruikt. Als u overgang van Implementatiemodel tooproduction, wordt u aangeraden toepassingen zoals Hallo [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) als uw tweede factor indien mogelijk.
Meer informatie: [concept NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>MFA voorwaardelijke toegang voor SaaS-toepassingen

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Identificeer implementatiemodel gebruikers tootarget Hallo beleid. Deze gebruikers moeten zich in een groep tooscope Hallo voorwaardelijke toegang beveiligingsbeleid | [Configuratie van de SaaS-federatieve SSO](#saas-federated-sso-configuration) |
| SaaS-toepassing is al geconfigureerd |  |
| Gebruikers van de POC-fase zijn toohello toepassing al toegewezen |  |
| Referenties toohello Implementatiemodel gebruiker beschikbaar zijn |  |
| Implementatiemodel gebruiker is geregistreerd voor MFA. Via een telefoon met goede ontvangst | http://aka.MS/ssprsetup |
| Apparaat in het interne netwerk Hallo. IP-adres geconfigureerd in de interne adresbereik Hallo | Uw IP-adres vinden: https://www.bing.com/search?q=what%27s+my+ip |
| Apparaat in Hallo externe netwerk (een telefoon met behulp van het mobiele netwerk Hallo carrier van kunnen zijn) |  |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Ga tooAzure AD-beheerportal: blade voorwaardelijke toegang | [Azure AD-beheerportal: Voorwaardelijke toegang](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Maak beleid voor voorwaardelijke toegang:<br/>-Gebruikers van de PoC target onder 'Gebruikers en groepen'<br/>-Implementatiemodel doeltoepassing onder 'Cloud-apps'<br/>-Gericht op alle locaties, behalve vertrouwde die onder 'Voorwaarden'-"Locaties" > **Opmerking:** goedgekeurde IP-adressen zijn geconfigureerd in [Portal MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>-Multi-factor authentication-server onder 'Grant' vereisen | [Aan de slag met voorwaardelijke toegang in Azure Active Directory: configuratiestappen beleid](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Toegang van een toepassing binnen bedrijfsnetwerk | [Aan de slag met voorwaardelijke toegang in Azure Active Directory: Hallo beleid testen](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Toegang tot de toepassing van openbaar netwerk | [Aan de slag met voorwaardelijke toegang in Azure Active Directory: Hallo beleid testen](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Overwegingen

Als u federation gebruikt, kunt u Hallo lokale identiteitsprovider (IdP) toocommunicate Hallo binnen/buiten-bedrijfsnetwerk staat met claims. U kunt deze techniek gebruiken zonder toomanage Hallo lijst met IP-adressen die mogelijk complexe tooassess en beheren in grote organisaties. In dat de installatie, moet u rekening voor Hallo 'netwerk roaming'-scenario (een gebruiker de logboekregistratie van het interne netwerk Hallo en tijdens het aangemelde switches locaties bijvoorbeeld een restaurant) en zorg ervoor dat u Hallo implicaties begrijpt. Meer informatie: [cloudresources beveiligen met Azure multi-factor Authentication en AD FS: goedgekeurde IP-adressen voor federatieve gebruikers](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Beschermde identiteitsbeheer (PIM)

Geschatte tijd tooComplete: 15 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Hallo globale beheerder die deel van Hallo Implementatiemodel voor PIM uitmaken identificeren | [Aan de slag met Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Hallo globale beheerder die Hallo beveiligingsbeheerder fungeren zal identificeren | [Aan de slag met Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Andere beheerdersrollen in Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Optioneel: Controleer als globale beheerders Hallo e-mail hebben toegang tot tooexercise e-mailmeldingen in PIM | [Wat is Azure AD Privileged Identity Management?: Hallo rol activeringsinstellingen configureren](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Aanmelding toohttps://portal.azure.com als een globale beheerder (GA) en bootstrap Hallo PIM-blade. Hallo globale beheerder die in deze stap uitvoert is als Hallo beveiligingsbeheerder gemaakt.  Laten we deze acteur GA1 aanroepen | [Met behulp van de wizard Beveiliging Hallo in Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Globale beheerder Hallo identificeren en deze te verplaatsen van permanente tooeligible. Dit moet een beheerder van Hallo gebruikt in stap 1 voor de duidelijkheid zijn afzonderlijke. Laten we deze acteur GA2 aanroepen | [Azure AD Privileged Identity Management: Hoe tooadd of een gebruikersrol verwijderen](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Wat is Azure AD Privileged Identity Management?: Hallo rol activeringsinstellingen configureren](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Nu aanmelden als GA2 toohttps://portal.azure.com en wijzig 'Gebruikersinstellingen'. U ziet enkele opties zijn niet beschikbaar. | |
| In een nieuw tabblad en Hallo dezelfde sessie als stap 3, gaat u nu toohttps://portal.azure.com en Hallo PIM blade toohello dashboard toevoegen. | [Hoe tooactivate of deactiveren van rollen in Azure AD Privileged Identity Management: Hallo Privileged Identity Management-toepassing toevoegen](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Aanvragen van de rol van algemeen beheerder toohello activering | [Hoe tooactivate of deactiveren van rollen in Azure AD Privileged Identity Management: een rol activeren](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Houd er rekening mee dat als GA2 nooit aangemeld voor MFA, registratie voor Azure MFA moet worden |  |
| Ga terug toohello oorspronkelijke tabblad in stap 3 en klik op Hallo de knop Vernieuwen in de browser Hallo. Houd er rekening mee dat u nu toegang toochange hebt 'Gebruikersinstellingen' | |
| Eventueel, als uw globale beheerders e-mailbericht is ingeschakeld, u kunt GA1 en GA2 van postvak in en Hallo melding van Hallo-rol wordt geactiveerd |  |
| 8 Hallo controlegeschiedenis controleren en zien Hallo rapport tooconfirm Hallo onrechtmatige uitbreiding van GA2 wordt weergegeven. | [Wat is Azure AD Privileged Identity Management?: rol controleactiviteit](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Overwegingen

Deze mogelijkheid is onderdeel van Azure AD Premium-P2 en/of EMS E5

## <a name="discovering-risk-events"></a>Risico's detecteren

Geschatte tijd tooComplete: 20 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Apparaten met Tor browser gedownload en geïnstalleerd | [Tor Browser downloaden](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Toegang tooPOC toodo Hallo gebruikersaanmelding | [Playbook voor Azure Active Directory: Identity Protection](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Open tor-browser | [Tor Browser downloaden](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Meld u bij toohttps://myapps.microsoft.com Hello POC-gebruikersaccount | [Azure Active Directory: Identity Protection playbook: Risicogebeurtenissen simuleren](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Wacht 5-7 minuten |  |
| Meld u aan als een globale beheerder toohttps://portal.azure.com en Hallo Identity Protection blade geopend | https://aka.MS/aadipgetstarted |
| Open Hallo risico gebeurtenissen blade. Er is een item onder 'Aanmeldingen vanaf anonieme IP-adressen'  | [Azure Active Directory: Identity Protection playbook: Risicogebeurtenissen simuleren](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Overwegingen

Deze mogelijkheid is onderdeel van Azure AD Premium-P2 en/of EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Aanmelden risico beleid implementeren

Geschatte tijd tooComplete: 10 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Apparaten met Tor browser gedownload en geïnstalleerd | [Tor Browser downloaden](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Toegang als een Implementatiemodel toodo Hallo aanmelding van gebruiker testen |  |
| Implementatiemodel gebruiker is geregistreerd met MFA. Zorg ervoor dat toouse een telefoon met goede ontvangst | Bouwsteen: [Azure multi-factor Authentication met telefoongesprekken](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| Meld u aan als een globale beheerder toohttps://portal.azure.com blade en open Hallo Identity Protection | https://aka.MS/aadipgetstarted |
| Een beleid voor aanmelden risico als volgt inschakelen:<br/>-Toegewezen aan: Implementatiemodel gebruiker<br/>-Voorwaarden: Aanmelden risico gemiddeld of hoger (aanmelden vanaf anonieme locatie wordt beschouwd als een gemiddeld risiconiveau)<br/>-Besturingselementen: MFA vereisen | [Azure Active Directory: Identity Protection playbook: aanmelden risico](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Open tor-browser | [Tor Browser downloaden](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Meld u bij toohttps://myapps.microsoft.com Hello PoC-gebruikersaccount |  |
| Kennisgeving Hallo MFA uitdaging | [Aanmelden-ervaringen met Azure AD Identity Protection: riskant aanmelden herstel](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Overwegingen

Deze mogelijkheid is onderdeel van Azure AD Premium-P2 en/of EMS E5. meer informatie over de risico's gaat u naar toolearn: [risicogebeurtenissen Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Gebaseerde certificaatverificatie configureren

Geschatte tijd toocomplete: 20 minuten

### <a name="pre-requisites"></a>Vereisten

| Vereiste | Resources |
| --- | --- |
| Apparaat met gebruikerscertificaat ingericht (Windows, iOS of Android) van Enterprise PKI | [Gebruikerscertificaten implementeren](https://msdn.microsoft.com/library/cc770857.aspx) |
| Azure AD-domein gefedereerd met AD FS | [Azure AD Connect en federatie](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Overzicht van Active Directory Certificate Services](https://technet.microsoft.com/library/hh831740.aspx)|
| Voor iOS-apparaten Microsoft Authenticator-app hebt geïnstalleerd | [Aan de slag met Hallo Microsoft Authenticator-app](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Stappen

| Stap | Resources |
| --- | --- |
| "Verificatie met gebruikerscertificaat" op de AD FS inschakelen | [Verificatiebeleid configureren: tooconfigure primaire verificatie globaal in Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Optioneel: Authenticatie via certificaat inschakelen in Azure AD voor Exchange ActiveSync-clients | [Aan de slag met verificatie op basis van certificaten in Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Navigeer tooAccess Configuratiescherm en verificatie met gebruikerscertificaat | https://myapps.Microsoft.com |

### <a name="considerations"></a>Overwegingen

meer informatie over aanvullende opmerkingen van deze implementatie gaat u naar toolearn: [ADFS: verificatie met Azure AD & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Bezit van gebruikerscertificaat moet worden bewaakt. Door op het beheren van apparaten of met PINCODE in geval van smartcards.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
