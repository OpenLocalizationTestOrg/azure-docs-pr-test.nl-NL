---
title: aaaHow tooprovide veilige externe toegang tooon-premises apps
description: Bevat informatie over hoe toouse Azure AD-toepassingsproxy tooprovide veilige externe toegang tooyour lokale apps.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen

Werknemers wilt vandaag toobe productief op welke plaats, op elk gewenst moment en vanaf elk apparaat. Ze willen toowork op hun eigen apparaten, of deze nu tablets en telefoons en laptops. En ze verwachten toobe kunnen tooaccess hun toepassingen, zowel SaaS-apps in de cloud Hallo en zakelijke apps on-premises. Toegang verlenen tooon-premises toepassingen is traditioneel betrokken virtuele particuliere netwerken (VPN's) of demilitarized zones (DMZ's). Niet alleen zijn deze oplossingen complex en moeilijk toomake beveiligd, maar ze zijn kostbare tooset en beheren.

Er is een betere manier!

Een moderne werknemers in mobile eerst Hallo, wereld cloud eerste moet moderne RAS-oplossing. Azure AD-toepassingsproxy is een functie van Azure Active Directory biedt externe toegang als een service. Dit betekent dat het is gemakkelijk toodeploy, gebruiken en beheren.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Wat is Azure Active Directory-toepassingsproxy?
Azure AD-toepassingsproxy biedt eenmalige aanmelding (SSO) en veilige externe toegang voor webtoepassingen die lokaal worden gehost. Sommige apps die u zou willen toopublish omvatten SharePoint-sites, Outlook Web Access of andere LOB webtoepassingen hebt. Deze lokale web toepassingen worden geïntegreerd met Azure AD Hallo dezelfde identiteit en platform dat wordt gebruikt door O365 te beheren. Eindgebruikers hebben toegang tot uw lokale toepassingen Hallo dezelfde manier als die ze toegang O365 en andere SaaS-apps tot worden geïntegreerd met Azure AD. Of u kunt geen toochange Hallo netwerkinfrastructuur VPN-tooprovide van deze oplossing voor uw gebruikers vereisen.

## <a name="why-is-application-proxy-a-better-solution"></a>Waarom is een betere oplossing toepassingsproxy?
Azure AD-toepassingsproxy biedt een eenvoudige, rendabele en veilige externe toegang oplossing tooall uw on-premises toepassingen.

Azure AD-toepassingsproxy is:

* **Eenvoudige**
   * Of u kunt geen toochange uw toowork toepassingen bijwerken met toepassingsproxy. 
   * Uw gebruikers krijgen een consistente verificatie-ervaring. Hallo MyApps portal tooget eenmalige aanmelding tooboth SaaS-apps in Hallo cloud en uw apps on-premises kan worden gebruikt. 
* **Beveiligen**
   * Wanneer u uw apps met behulp van Azure AD-toepassingsproxy publiceert, kunt u profiteren van Hallo uitgebreide autorisatie besturingselementen en beveiligingsanalyse in Azure. U ophalen cloud-scale beveiligings- en Azure-beveiligingsfuncties zoals voorwaardelijke toegang en in twee stappen verificatie.
   * U hebt geen tooopen alle binnenkomende verbindingen via uw firewall toogive uw gebruikers externe toegang. 
* **Rendabele**
   * Toepassingsproxy werkt in Hallo cloud, zodat u tijd en geld kunt opslaan. Oplossingen on-premises vereisen tooset up doorgaans te onderhouden DMZ's, randservers of andere complexe infrastructuren.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Wat voor soort toepassingen werken met toepassingsproxy?
Met Azure AD-toepassingsproxy hebt u toegang tot verschillende soorten interne toepassingen:

* Webtoepassingen die gebruikmaken van [geïntegreerde Windows-verificatie](active-directory-application-proxy-sso-using-kcd.md) voor verificatie  
* Webtoepassingen die gebruikmaken van op basis van formulieren of [op basis van een koptekst](application-proxy-ping-access.md) toegang  
* Web-API's die u wilt dat tooexpose toorich toepassingen op verschillende apparaten  
* Toepassingen die worden gehost achter een [extern bureaublad-Gateway](application-proxy-publish-remote-desktop.md)  
* Rich client-apps die zijn geïntegreerd met Hallo Active Directory Authentication Library (ADAL)

## <a name="how-does-application-proxy-work"></a>Hoe werkt de toepassingsproxy?
Er zijn twee onderdelen dat u tooconfigure toomake toepassingsproxy werk nodig: een connector en een extern eindpunt. 

Hallo-connector is een lichtgewicht agent die zich op een Windows-Server in uw netwerk. Hallo connector vereenvoudigt het Hallo-netwerkverkeer van Hallo service voor toepassingsproxy op Hallo cloud tooyour toepassing on-premises. Uitgaande verbindingen wordt alleen gebruikt zodat u niet tooopen poorten voor inkomend verkeer hebt of iets in Hallo DMZ plaatsen. Hallo-connectors zijn staatloze en ophalen uit de cloud Hallo indien nodig. Voor meer informatie over connectors worden, zoals hoe ze verdelen en worden geverifieerd, Zie [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md). 

Hallo Extern eindpunt is hoe uw gebruikers bereiken voor uw toepassingen terwijl buiten uw netwerk. Ze kunnen ofwel gaat u rechtstreeks tooan externe URL die u bepaalt of toegang te krijgen tot de toepassing hello via Hallo MyApps portal. Wanneer gebruikers gaan tooone van deze eindpunten, bevindt deze zich verifiëren bij Azure AD en vervolgens worden gerouteerd via Hallo connector toohello on-premises toepassing.

 ![Toepassingsproxy AzureAD-diagram](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. Hallo gebruiker toegang heeft tot de toepassing hello via Hallo service voor toepassingsproxy en gerichte toohello Azure AD-aanmeldingspagina tooauthenticate is.
2. Na een geslaagde aanmelden, wordt een token gegenereerd en verzonden toohello-clientapparaat.
3. Hallo-client verzendt Hallo token toohello Application Proxy-service, die wordt opgehaald Hallo UPN (user Principal name), en beveiliging principal name (SPN) van het Hallo-token, stuurt vervolgens Hallo aanvraag toohello Application Proxy connector.
4. Als u eenmalige aanmelding hebt geconfigureerd, voert Hallo connector vereist namens de gebruiker Hallo aanvullende verificatie.
5. Hallo-connector verzendt Hallo aanvraag toohello on-premises toepassing.  
6. Hallo-antwoord wordt verzonden via Application Proxy-service en connector toohello gebruiker.

### <a name="single-sign-on"></a>Eenmalige aanmelding
Azure AD-toepassingsproxy biedt eenmalige aanmelding (SSO) tooapplications die gebruikmaken van geïntegreerde Windows-verificatie (IWA) of de claimbewuste toepassingen. Als uw toepassing gebruikmaakt van IWA, imiteert toepassingsproxy Hallo-gebruiker met behulp van Kerberos-beperkte overdracht tooprovide eenmalige aanmelding. Als u een claimbewuste toepassing die door Azure Active Directory wordt vertrouwd hebt, werkt eenmalige aanmelding omdat Hallo gebruiker is al geverifieerd door Azure AD.

Zie voor meer informatie over Kerberos [alle gewenste tooknow over Kerberos-beperkt delegatie (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Apps beheren
Een van uw app met toepassingsproxy wordt gepubliceerd, kunt u deze beheren als elke andere enterprise-app in hello Azure-portal. U kunt u Azure Active Directory-beveiligingsfuncties zoals voorwaardelijke toegang en in twee stappen verificatie, gebruikersmachtigingen beheren en Hallo huisstijl voor uw app aanpassen. 

## <a name="get-started"></a>Aan de slag

Voordat u Application Proxy configureert, controleert u of er een ondersteunde [Azure Active Directory-editie](https://azure.microsoft.com/pricing/details/active-directory/) en een Azure AD-directory waarvoor u een globale beheerder bent.

Aan de slag met toepassingsproxy in twee stappen:

1. [Toepassingsproxy inschakelen en configureren van Hallo connector](active-directory-application-proxy-enable.md).    
2. [Toepassingen publiceren](active-directory-application-proxy-publish.md) -gebruik Hallo tooget wizard snel en eenvoudig uw lokale apps gepubliceerde en toegankelijk is op afstand.

## <a name="whats-next"></a>Volgende stappen
Nadat u uw eerste app publiceert, vindt u veel meer u met toepassingsproxy doen kunt.

* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Toepassingen publiceren met uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md)
* [Meer informatie over Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md)
* [Werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md) 
* [Een aangepaste startpagina ingesteld](application-proxy-office365-app-launcher.md)

Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)

