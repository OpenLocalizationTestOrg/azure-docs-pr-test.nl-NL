---
title: aaaHow toepassingen worden tooAzure Active Directory toegevoegd.
description: Dit artikel wordt beschreven hoe toepassingen tooan exemplaar van Azure Active Directory worden toegevoegd.
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Hoe en waarom toepassingen tooAzure AD worden toegevoegd
Een van de dingen in eerste instantie puzzling wanneer u een lijst met toepassingen in uw exemplaar van Azure Active Directory bekijkt hello is waar Hallo toepassingen vandaan komen en waarom ze zijn er begrijpen.  In dit artikel biedt een hoog niveau overzicht van hoe toepassingen worden weergegeven in de directory Hallo en bieden u context die u u helpt begrijpen hoe een toepassing is geleverd toobe in uw directory.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>Welke services biedt Azure AD tooapplications?
Toepassingen toegevoegd tooAzure AD tooleverage een of meer van Hallo-services biedt.  Deze services zijn onder andere:

* App-verificatie en autorisatie
* Verificatie en autorisatie
* Eenmalige aanmelding (SSO) met behulp van Federatie of wachtwoord
* Gebruikers inrichten & synchronisatie
* Toegangsbeheer op basis van rollen; Gebruik Hallo directory toodefine rollen tooperform toepassingsrollen gebaseerd autorisatie controles in een app.
* oAuth-autorisatieservices (gebruikt door Office 365 en andere Microsoft-apps tooauthorize toegang tooAPIs /-bronnen).
* Toepassingen publiceren en & proxyverkeer; Publiceren van een app van een particulier netwerk toohello internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Hoe worden toepassingen weergegeven in de directory Hallo?
Toepassingen worden weergegeven in hello Azure AD dat gebruikmaakt van objecten 2: een object voor de toepassing en een service-principal-object.  Er is een object van de toepassing, geregistreerd in een "home" / 'eigenaar' of 'publiceren' directory en een of meer service-principal-objecten die de toepassing hello in elke directory het fungeert.  

Hallo toepassingsobject beschrijft Hallo app tooAzure AD (Hallo multitenant-service) en bevatten mogelijk geen van de volgende Hallo: (*Opmerking*: dit is geen uitputtende lijst.)

* Naam, Logo & uitgever
* Geheimen (symmetrische en/of asymmetrische sleutels gebruikt tooauthenticate Hallo app)
* API-afhankelijkheden (oAuth)
* API's / resources/bereiken gepubliceerd (oAuth)
* App-functies (RBAC)
* SSO-metagegevens en -configuratie (SSO)
* Gebruikers inrichten metagegevens en configuratie
* Proxy-metagegevens en configuratie

Hallo-service-principal is een record van de toepassing hello in elke map, waar de toepassing hello fungeert met inbegrip van de basismap.  Hallo service-principal:

* Verwijst terug tooan application-object via Hallo app-id-eigenschap
* Registreert lokale gebruiker en groep-app-roltoewijzingen
* Registreert lokale gebruiker en de Administrator-machtigingen verleend toohello app
  * Bijvoorbeeld: machtiging voor Hallo app tooaccess een bepaalde gebruikers e-mailadres
* Records lokaal beleid, met inbegrip van beleid voor voorwaardelijke toegang
* Registreert lokale alternatieve lokale instellingen voor een app
  * Claimregels voor transformatie
  * Kenmerktoewijzingen (gebruikersinrichting)
  * Specifieke app-functies voor de tenantsleutel (als Hallo app aangepaste rollen ondersteunt)
  * Naam/het Logo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Een diagram van toepassingsobjecten en service-principals op mappen
![Een diagram illustreert hoe toepassing objecten en service-principals bestaande met exemplaren van Azure AD.][apps_service_principals_directory]

Zoals u in de bovenstaande Hallo diagram zien kunt.  Microsoft onderhoudt twee directory's (op Hallo links) intern wordt gebruikt toopublish toepassingen.

* Één voor Microsoft-Apps (directory voor services van Microsoft)
* Een voor vooraf geïntegreerde 3e partij Apps (App-galerie directory)

Toepassing uitgevers/leveranciers die met Azure AD integreren zijn vereiste toohave een publishing map.  (Sommige SAAS Directory).

Toepassingen die u zelf toevoegen omvatten:

* Apps die u hebt ontwikkeld (geïntegreerd met AAD)
* Apps die u verbonden voor eenmalige aanmelding
* Apps die u hebt gepubliceerd met behulp van hello Azure AD-toepassingsproxy.

### <a name="a-couple-of-notes-and-exceptions"></a>Een aantal opmerkingen en uitzonderingen
* Niet alle service-principals wijst back tooapplication objecten.  Huh? Wanneer u Azure AD oorspronkelijk is opgebouwd opgegeven Hallo services tooapplications zijn veel meer beperkte en Hallo service-principal is voldoende voor het tot stand brengen van een app-identiteit.  Hallo oorspronkelijke service-principal is dichter in de vorm toohello Windows Server Active Directory-serviceaccount.  Om deze reden is nog steeds mogelijk toocreate Hallo service-principals met behulp van Azure AD PowerShell zonder eerst te maken een application-object.  Hallo Graph API vereist een app-object voordat u een service-principal maken.
* Niet alle Hallo gegevens zoals hierboven beschreven is momenteel beschikbaar gemaakt via een programma.  de volgende Hallo zijn alleen beschikbaar in Hallo gebruikersinterface:
  * Claimregels voor transformatie
  * Kenmerktoewijzingen (gebruikersinrichting)
* Voor meer gedetailleerde informatie over de service-principal Hallo en Raadpleeg toohello Azure AD Graph REST-API-naslagdocumentatie toepassingsobjecten.  *Hint*: hello Azure AD Graph API-documentatie is Hallo dichtstbijzijnde ding tooa schemaverwijzing voor Azure AD die momenteel beschikbaar is.  
  * [Toepassing](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Service-Principal](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Hoe worden apps toomy Azure AD-exemplaar toegevoegd?
Er zijn veel manieren die een app tooAzure AD kan worden toegevoegd:

* Een app toevoegen van Hallo [App-galerie van Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Meld u aan van/naar een 3rd Party App is geïntegreerd met Azure Active Directory (bijvoorbeeld: [Smartsheet](https://app.smartsheet.com/b/home) of [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * Tijdens de aanmelding omhoog/gebruikers zijn gestelde toogive machtiging toohello app tooaccess hun profiel en andere machtigingen.  de eerste persoon toogive Hallo toestemming oorzaken een service-principal die Hallo app toobe toegevoegde toohello directory vertegenwoordigt.
* Aanmelding van/naar Microsoft online services, zoals [Office 365](http://products.office.com/)
  * Wanneer u zich abonneert tooOffice 365 beginnen met een proefabonnement of meer service-principals verschillende services die worden gebruikt toodeliver Hallo-functionaliteit die is gekoppeld aan Office 365 in Hallo directory Hallo die zijn gemaakt.
  * Sommige Office 365-services, zoals SharePoint maken service-principals op een veilige basis continu tooallow-communicatie tussen onderdelen, waaronder de werkstromen.
* Een app die u ontwikkelt toevoegen in Azure Management Portal Zie Hallo: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Toevoegen aan een app die u ontwikkelt met Visual Studio Zie:
  * [ASP.Net-verificatiemethoden](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Verbonden Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Toevoegen van een app toouse toouse hello [Azure AD-toepassingsproxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Verbinding maken met een app voor eenmalige aanmelding via SAML of SSO-wachtwoord
* Vele andere met inbegrip van verschillende ervaringen met de ontwikkelaar in Azure en/in API explorer optreedt tussen ontwikkelaars centers

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Wie de machtiging tooadd toepassingen toomy Azure AD-exemplaar heeft?
Alleen globale beheerders kunnen:

* Apps van app-galerie van Azure AD hello (vooraf geïntegreerde 3e partij Apps) toevoegen
* Een app publiceren met hello Azure AD-toepassingsproxy

Alle gebruikers in uw directory zijn rechten tooadd toepassingen die ze ontwikkelt en discreet via welke toepassingen ze share/Verleen toegang tootheir organisatiegegevens.  *Gebruiker aanmelden omhoog/tooan app onthouden en het verlenen van machtigingen kunnen leiden tot een service-principal wordt gemaakt.*

Deze in eerste instantie geluid betreffende mogelijk, maar houd Hallo volgende in gedachten:

* Apps zijn kunnen tooleverage Windows Server Active Directory voor gebruikersverificatie jaren zonder Hallo toepassing toobe geregistreerd/vastgelegd in de directory Hallo.  Nu Hallo organisatie hebben een zichtbaarheid tooexactly verbeterde wordt hoeveel apps gebruikt Hallo directory en what for.
* U hoeft voor beheer-app publiceren/registratieproces aangestuurd.  Met Active Directory Federation Services is het waarschijnlijk dat een beheerder had tooadd een app als een relying party namens ontwikkelaars.  Ontwikkelaars kunnen nu self-service.
* Gebruikers die zich in/up tooapps met behulp van hun organisatie-account voor zakelijke doeleinden is goed.  Als ze later niet meer Hallo organisatie verliest ze tootheir toegangsaccount in Hallo toepassing die ze gebruikten.
* Is een record van welke gegevens die aan de toepassing een goed is is gedeeld.  Gegevens zijn meer dan ooit vervoerbare en met een lege record van wie welke gegevens gedeeld met welke toepassingen zijn nuttig.
* Apps die gebruikmaken van Azure AD voor oAuth bepalen precies welke machtigingen dat gebruikers zich kunnen toogrant tooapplications en welke machtigingen een tooagree beheerder om te vereist.  Deze vanzelf alleen beheerders toestemming kunt geven toolarger scopes en meer machtigingen.
* Gebruikers toevoegen en zodat apps tooaccess die hun gegevens zijn gecontroleerd gebeurtenissen Hallo controlerapporten binnen hello Azure Management portal toodetermine te geven hoe een app is toegevoegd toohello directory.

**Opmerking:** *Microsoft zelf is uitgevoerd met behulp van de standaardconfiguratie Hallo nu aantal maanden.*

Met alle die deze is mogelijk tooprevent gebruikers in uw directory van het toevoegen van toepassingen en uit te oefenen beslissen over welke informatie ze met toepassingen delen door het wijzigen van de configuratie van de Directory in hello Azure-beheerportal.  Hallo kan volgende configuratie worden benaderd binnen hello Azure Management portal op het tabblad voor uw Directory 'Configureren'.

![Een schermopname van Hallo gebruikersinterface voor het configureren van geïntegreerde app-instellingen][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
Meer informatie over het tooadd toepassingen tooAzure AD en hoe tooconfigure services voor apps.

* Ontwikkelaars: [meer hoe een toepassing met AAD toointegrate](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Ontwikkelaars: [voorbeeldcode voor apps die zijn geïntegreerd met Azure Active Directory op GitHub bekijken](https://github.com/AzureADSamples)
* Ontwikkelaars en IT-professionals: [Hallo REST-API-documentatie voor hello Azure Active Directory Graph API doornemen](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* IT-professionals: [meer informatie over hoe Azure Active Directory toouse vooraf geïntegreerde toepassingen van App-galerie Hallo](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* IT-professionals: [zelfstudies voor het configureren van specifieke vooraf geïntegreerde apps](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* IT-professionals: [meer informatie over hoe toopublish een app met Azure Active Directory-toepassingsproxy Hallo](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Zie ook
* [Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
