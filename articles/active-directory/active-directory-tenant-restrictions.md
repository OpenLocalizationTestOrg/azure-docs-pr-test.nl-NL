---
title: aaaManage toegang toocloud apps door het beperken van tenants - Azure | Microsoft Docs
description: Hoe toouse Tenant beperkingen toomanage welke gebruikers toegang apps tot hebben gebaseerd op hun Azure AD-tenant.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Beperkingen van de Tenant toomanage toegang tooSaaS cloud-toepassingen gebruiken

Grote organisaties die Leg de nadruk op beveiliging wilt toomove toocloud services zoals Office 365, maar moeten tooknow die hun gebruikers alleen toegang tot bronnen goedgekeurd. Traditioneel beperken bedrijven domeinnamen of IP-adressen wanneer hij of zij wil toomanage toegang Deze aanpak is mislukt in een wereld waar SaaS-apps worden gehost in een openbare cloud, op gedeelde domeinnamen zoals outlook.office.com en login.microsoftonline.com uitgevoerd. Het blokkeren van deze adressen zou voorkomen dat gebruikers toegang tot de Outlook op Hallo web volledig, in plaats van alleen beperken tooapproved identiteiten en resources.

Azure Active Directory-oplossing toothis uitdaging is een functie voor Tenant-beperkingen. Tenant beperkingen kunnen organisaties toocontrol toegang tooSaaS cloudtoepassingen, op basis van hello Azure AD-tenant Hallo toepassingen gebruiken voor eenmalige aanmelding. U kunt bijvoorbeeld tooallow toegang tooyour van organisatie Office 365-toepassingen, zonder dat er toegang tooother organisaties exemplaren van deze toepassingen.  

Beperkingen van de tenant geeft organisaties Hallo mogelijkheid toospecify Hallo lijst met tenants of gebruikers tooaccess zijn toegestaan. Vervolgens Azure AD hebben alleen toegang toothese toegestaan tenants.

In dit artikel is gericht op de Tenant beperkingen voor Office 365, maar de functie Hallo moet samenwerken met elke SaaS-cloud-app die gebruikmaakt van moderne verificatieprotocollen met Azure AD voor eenmalige aanmelding. Als u de SaaS-apps met een andere Azure AD-van Hallo tenant die wordt gebruikt door Office 365 tenant gebruikt, zorg ervoor dat alle vereiste tenants zijn toegestaan. Zie voor meer informatie over SaaS-cloud-apps, Hallo [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Hoe werkt het?

Hallo algehele omvat oplossing Hallo volgende onderdelen: 

1. **Azure AD** – als hello `Restrict-Access-To-Tenants: <permitted tenant list>` aanwezig, Azure AD is alleen problemen beveiligingstokens voor Hallo tenants toegestaan. 

2. **On-premises proxy serverinfrastructuur** – een proxyapparaat geschikt voor SSL-inspectie geconfigureerde tooinsert Hallo header met Hallo lijst met tenants toegestaan in een verkeer dat is bestemd voor Azure AD. 

3. **Clientsoftware** – toosupport Tenant beperkingen, clientsoftware moet aanvragen tokens rechtstreeks vanuit Azure AD, zodat verkeer kan worden onderschept door de infrastructuur van webtoepassingsproxy Hallo. Beperkingen van de tenant wordt momenteel ondersteund door Office 365-toepassingen op basis van een browser en Office-clients als moderne verificatie (zoals OAuth 2.0) wordt gebruikt. 

4. **Moderne verificatie** : cloudservices moderne verificatie toouse Tenant beperkingen moeten gebruiken en toegang blokkeren tot tooall niet toegestaan tenants. Office 365 cloudservices moet geconfigureerde toouse moderne verificatieprotocollen standaard. Lees voor de meest recente informatie over Office 365-ondersteuning voor moderne verificatie Hallo [moderne authenticatie van Office 365 bijgewerkt](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Hallo volgende diagram illustreert Hallo op hoog niveau netwerkverkeer. SSL-inspectie is alleen vereist op verkeer tooAzure AD, niet toohello Office 365 cloudservices. Dit onderscheid is belangrijk omdat Hallo verkeersvolume voor de verificatie tooAzure AD doorgaans veel lager zijn dan verkeer volume tooSaaS toepassingen zoals Exchange Online en SharePoint Online is.

![Tenant-netwerkverkeer beperkingen - diagram](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Tenant beperkingen instellen

Er zijn twee stappen tooget gestart met Tenant-beperkingen. Hallo eerste stap is ervoor dat uw clients verbinding van de juiste adressen toohello maken kunnen toomake. Hallo tweede tooconfigure is uw proxy-infrastructuur.

### <a name="urls-and-ip-addresses"></a>URL's en IP-adressen

toouse Tenant beperkingen, uw clients moeten kunnen tooconnect toohello tooauthenticate Azure AD-URL's te volgen: login.microsoftonline.com login.microsoft.com en login.windows.net. Bovendien tooaccess Office 365, uw clients moeten kunnen tooconnect toohello FQDN's / URL's en IP-adressen die zijn gedefinieerd in [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Proxyconfiguratie en vereisten

Hallo na de configuratie is vereist tooenable Tenant beperkingen via uw proxy-infrastructuur. In deze richtlijnen is algemeen, raadpleegt u de documentatie van tooyour proxy leverancier voor specifieke implementatiestappen.

#### <a name="prerequisites"></a>Vereisten

- Hallo proxy moet kunnen tooperform SSL worden onderschept, HTTP-header invoegen en filter bestemmingen met FQDN's / URL's. 

- Hallo certificaatketen die worden aangeboden door Hallo-proxy voor SSL-communicatie moeten worden vertrouwd door clients. Bijvoorbeeld, als u certificaten van een interne PKI gebruikt, moet Hallo interne verlenende basis-CA-certificaat worden vertrouwd.

- Deze functie is opgenomen in Office 365-abonnementen, maar als u wilt dat toouse Tenant beperkingen toocontrol toegang tooother SaaS-apps vervolgens Azure AD Premium 1 licenties zijn vereist.

#### <a name="configuration"></a>Configuratie

Voor elke inkomende aanvraag toologin.microsoftonline.com, login.microsoft.com en login.windows.net, invoegen twee HTTP-headers: *Restrict Access aan Tenants* en *Restrict Access Context*.

Hallo-headers te Hallo volgende elementen bevatten: 
- Voor *Restrict Access aan Tenants*, een waarde van \<tenant lijst toegestaan\>, dit is een door komma's gescheiden lijst van tenants gewenste tooallow gebruikers tooaccess. Elk domein dat is geregistreerd bij een tenant kan worden gebruikt tooidentify hello tenant in deze lijst. Bijvoorbeeld toopermit tooboth Contoso en Fabrikam tenants toegang tot, naam/waarde-paar lijkt erop Hallo:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Voor *Restrict Access Context*, een waarde van een enkele map-ID, declareren waarover is Hallo Tenant beperkingen instellen. Bijvoorbeeld: toodeclare Contoso als Hallo-tenant die Hallo beleid Tenant beperkingen ingesteld, Hallo naam/waarde-paar ziet eruit als:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> U vindt de ID van uw directory in Hallo [Azure-portal](https://portal.azure.com). Meld u aan als beheerder, selecteer **Azure Active Directory**, selecteer daarna **eigenschappen**.

tooprevent gebruikers vanaf hun eigen HTTP-header met niet-goedgekeurde tenants invoegen, Hallo proxy moet tooreplace Hallo Restrict Access aan Tenants header als deze al aanwezig in de binnenkomende aanvraag Hallo is. 

Clients moeten geforceerde toouse Hallo proxy voor alle aanvragen toologin.microsoftonline.com login.microsoft.com en login.windows.net. Bijvoorbeeld, als bestanden voor het gebruikte toodirect clients toouse Hallo proxy, moet eindgebruikers niet kunnen tooedit of Hallo PAC bestanden uitschakelen.

## <a name="hello-user-experience"></a>Hallo-gebruikerservaring

Deze sectie toont Hallo ervaring voor eindgebruikers en beheerders.

### <a name="end-user-experience"></a>Eindgebruikerservaring

Een voorbeeld van de gebruiker zich op Hallo Contoso-netwerk, maar probeert tooaccess Hallo Fabrikam exemplaar van een gedeelde SaaS-toepassingen zoals Outlook online. Als Contoso een tenant niet is toegestaan voor het exemplaar is, ziet Hallo gebruiker Hallo na pagina:

![Toegang geweigerd-pagina voor gebruikers in tenants niet toegestaan](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Ervaring beheerder

Tijdens de configuratie van de beperkingen van de Tenant is voltooid op Hallo bedrijfsproxy infrastructuur, beheerders direct toegang tot Hallo Tenant beperkingen rapporten in hello Azure-portal. tooview Hallo rapporteert, toohello overzicht van Azure Active Directory-pagina gaan en vervolgens kijkt u onder andere mogelijkheden'.

Hallo beheerder voor de tenant Hallo opgegeven als Hallo beperkte toegang Context tenant kunt gebruiken in dit rapport toosee die alle aanmeldingen geblokkeerd vanwege Hallo beperkingen van de Tenant-beleid, met inbegrip van Hallo identiteit gebruikt en de doelmap Hallo-id 's

![Hello Azure portal tooview beperkt aanmeldpogingen gebruiken](./media/active-directory-tenant-restrictions/portal-report.png)

Net als andere rapporten in hello Azure-portal, kunt u filters toospecify Hallo bereik van uw rapport. U kunt filteren op een specifieke gebruiker, de toepassing, de client of het tijdsinterval.

## <a name="office-365-support"></a>Ondersteuning voor Office 365

Office 365-toepassingen moeten voldoen aan twee criteria toofully ondersteuning Tenant beperkingen:

1. Hallo-client gebruikt ondersteuning biedt voor moderne verificatie
2. Moderne verificatie is ingeschakeld als Hallo standaardverificatieprotocol voor Hallo-cloudservice.

Raadpleeg te[moderne authenticatie van Office 365 bijgewerkt](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) voor de meest recente informatie Hallo waarop Office clients momenteel moderne verificatie ondersteunen. Deze pagina bevat ook koppelingen tooinstructions voor het inschakelen van moderne verificatie op specifieke Exchange Online en Skype voor bedrijven Online tenants. Moderne verificatie is al in SharePoint Online standaard ingeschakeld.

Beperkingen van de tenant wordt momenteel ondersteund door Office 365-browser gebaseerde toepassingen (Office-Portal, Yammer SharePoint Hallo sites, Outlook op Hallo Web, enz.). Voor Rich clients (Outlook, Skype voor bedrijven, Word, Excel, PowerPoint, enz.) Beperkingen van de tenant kunnen alleen worden afgedwongen wanneer moderne verificatie wordt gebruikt.  

Outlook en Skype voor bedrijven-clients die moderne verificatie ondersteunen nog steeds kunnen toouse verouderde protocollen tegen tenants waarop moderne verificatie niet is ingeschakeld zijn, effectief Tenant beperkingen omzeilen. Voor Outlook op Windows, kunnen klanten ervoor kiezen tooimplement beperkingen zo wordt voorkomen dat eindgebruikers niet-goedgekeurde e-mail-accounts tootheir profielen toe te voegen. Zie bijvoorbeeld Hallo [Voorkom het toevoegen van niet-standaard Exchange-accounts](http://gpsearch.azurewebsites.net/default.aspx?ref=1) instellen via Groepsbeleid. Voor Outlook op niet-Windows-platforms, en voor Skype voor bedrijven op alle platforms is volledige ondersteuning voor de beperkingen van de Tenant momenteel niet beschikbaar.

## <a name="testing"></a>Testen

Als u tootry uit Tenant beperkingen wilt voordat u deze voor uw hele organisatie implementeert, er zijn twee opties: een benadering op basis van een host met een hulpprogramma zoals Fiddler of een gefaseerde implementatie van de proxy-instellingen.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler voor een host gebaseerde methode

Fiddler is een gratis web proxy die kan worden gebruikt toocapture en HTTP/HTTPS-verkeer, inclusief invoegen HTTP-headers wijzigen foutopsporing. tooconfigure Fiddler tootest Tenant beperkingen, Voer Hallo stappen te volgen:

1.  [Download en installeer Fiddler](http://www.telerik.com/fiddler).
2.  Configureer Fiddler toodecrypt HTTPS-verkeer [Fiddler van help-documentatie](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configureer Fiddler tooinsert hello *Restrict Access aan Tenants* en *Restrict Access Context* headers met behulp van aangepaste regels:
  1. Selecteer in het foutopsporingsprogramma Hallo Fiddler Web, Hallo **regels** menu en selecteer **regels aanpassen...** tooopen hello CustomRules-bestand.
  2. Toevoegen van de volgende regels aan begin Hallo HALLO hallo *OnBeforeRequest* functie. Vervang \<domein van de tenant\> met een domein geregistreerd bij uw tenant, bijvoorbeeld: contoso.onmicrosoft.com. Vervang \<map-ID\> met Azure AD-GUID-id van uw tenant.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Als u tooallow meerdere tenants moet, gebruikt u een door komma's tooseparate hello tenant namen. Bijvoorbeeld:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Opslaan en sluiten Hallo CustomRules bestand.

Nadat u Fiddler hebt geconfigureerd, kunt u verkeer vastleggen door te gaan toohello **bestand** menu en selecteer **verkeer vastleggen**.

### <a name="staged-rollout-of-proxy-settings"></a>Gefaseerde rollout van proxy-instellingen

Afhankelijk van het Hallo-mogelijkheden van uw infrastructuur van webtoepassingsproxy, hebt u mogelijk kunnen toostage Hallo rollout van instellingen tooyour gebruikers. Hier volgen een aantal geavanceerde opties voor overweging:

1.  PAC bestanden toopoint test gebruikers tooa test proxy-infrastructuur gebruiken, bij een normale gebruiker doorgaan toouse Hallo productie proxy-infrastructuur.
2.  Bepaalde proxyservers kunnen ondersteuning voor verschillende configuraties met behulp van groepen.

Raadpleeg tooyour proxy server-documentatie voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [moderne authenticatie van Office 365 bijgewerkt](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Bekijk Hallo [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
