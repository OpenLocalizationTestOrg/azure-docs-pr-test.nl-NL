---
title: aaaSingle aanmelding met toepassingsproxy | Microsoft Docs
description: Bevat informatie over hoe tooprovide eenmalige aanmelding met Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Kerberos-beperkte delegatie voor eenmalige aanmelding tooyour apps met toepassingsproxy

U kunt eenmalige aanmelding bieden voor on-premises toepassingen zijn gepubliceerd via toepassingsproxy die zijn beveiligd met geïntegreerde Windows-verificatie. Deze toepassingen vereisen een Kerberos-ticket voor toegang. Toepassingsproxy gebruikt Kerberos-beperkt delegatie (KCD) toosupport deze toepassingen. 

U kunt eenmalige aanmelding tooyour-toepassingen die gebruikmaken van geïntegreerde Windows-verificatie (IWA) door middel van een machtiging voor toepassingsproxy-connectors in Active Directory: gebruikers tooimpersonate inschakelen. Hallo-connectors met deze machtiging toosend en tokens namens hen ontvangen.

## <a name="how-single-sign-on-with-kcd-works"></a>Hoe eenmalige aanmelding met KCD werkt
Dit diagram wordt Hallo stroom uitgelegd wanneer een gebruiker probeert een on-premises-toepassing die gebruikmaakt van geïntegreerde Windows-tooaccess.

![Stroomdiagram van Microsoft AAD-verificatie](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. Hallo gebruiker voert Hallo URL tooaccess Hallo on-premises toepassing via toepassingsproxy.
2. Toepassingsproxy leidt Hallo aanvraag tooAzure AD authentication services toopreauthenticate. Azure AD van toepassing op dit moment voor eventuele van toepassing verificatie en autorisatie-beleidsregels, zoals meervoudige verificatie. Als het Hallo-gebruiker is gevalideerd, wordt Azure AD een token wordt gemaakt en verzendt deze toohello gebruiker.
3. Hallo gebruiker Hallo token tooApplication Proxy is geslaagd.
4. Toepassingsproxy valideert Hallo token haalt UPN (User Principal Name) van het Hallo en vervolgens verzendt aanvraag Hallo Hallo UPN en Service Principal Name (SPN) toohello Connector via een beveiligd kanaal voor zowel geverifieerde Hallo.
5. Hallo Connector voert Kerberos-beperkt delegatie (KCD)-onderhandeling met Hallo on-premises AD, Hallo gebruiker tooget een Kerberos-token toohello toepassing imiteert.
6. Active Directory wordt Kerberos-token voor Hallo toepassing toohello Connector Hallo verzonden.
7. Hallo Connector verzendt Hallo oorspronkelijke aanvraag toohello toepassingsserver, die Kerberos-token Hallo die deze van AD ontvangen.
8. Hallo-toepassing verzendt hello antwoord toohello Connector, die vervolgens wordt geretourneerd toohello Application Proxy-service en tot slot toohello gebruiker.

## <a name="prerequisites"></a>Vereisten
Voordat u aan de slag met eenmalige aanmelding voor geïntegreerde Windows-toepassingen, controleert u of uw omgeving gereed Hello instellingen en configuraties te volgen:

* Toouse zijn ingesteld door uw apps, zoals SharePoint Web-apps, geïntegreerde Windows-verificatie. Zie voor meer informatie [ondersteuning voor Kerberos-verificatie inschakelen](https://technet.microsoft.com/library/dd759186.aspx), of voor SharePoint-Zie [plannen voor Kerberos-verificatie in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Alle apps hebben [Service Principal Names](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* Hallo-server actief Hallo Connector en de Hallo app Hallo server zijn verbonden met het domein en deel uit van Hallo hetzelfde domein of in vertrouwde domeinen. Zie voor meer informatie over domein [lid worden van een Computer tooa domein](https://technet.microsoft.com/library/dd807102.aspx).
* Hallo-server waarop Hallo Connector wordt uitgevoerd heeft toegang tot tooread Hallo TokenGroupsGlobalAndUniversal kenmerk voor gebruikers. Deze instelling is mogelijk beïnvloed door beveiliging Hallo omgeving beperken.

### <a name="configure-active-directory"></a>Active Directory configureren
Hallo Active Directory-configuratie varieert, afhankelijk van of uw Application Proxy connector en de toepassingsserver Hallo zich in hetzelfde domein Hallo of niet.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Connector en de toepassingsserver in Hallo hetzelfde domein
1. Ga te in Active Directory**extra** > **gebruikers en Computers**.
2. Selecteer Hallo server Hallo-connector wordt uitgevoerd.
3. Met de rechtermuisknop en selecteer **eigenschappen** > **delegering**.
4. Selecteer **deze computer alleen overdracht toospecified services**. 
5. Onder **Services toowhich dit account gedelegeerde referenties kan presenteren** Hallo-waarde voor Hallo SPN-identiteit van de toepassingsserver Hallo toevoegen. Hierdoor kunnen Hallo Connector voor toepassingsproxy tooimpersonate gebruikers in AD tegen Hallo-toepassingen die zijn gedefinieerd in de lijst Hallo.

   ![Schermopname connector SVR eigenschappen](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Verbindingslijn en toepassingsservers in verschillende domeinen
1. Zie voor een lijst met vereisten voor het werken met KCD in meerdere domeinen, [Kerberos-beperkte delegatie in domeinen](https://technet.microsoft.com/library/hh831477.aspx).
2. Gebruik Hallo `principalsallowedtodelegateto` -eigenschap op Hallo Connector server tooenable Hallo toepassingsproxy toodelegate voor Hallo Connector-server. Hallo-toepassingsserver wordt `sharepointserviceaccount` en Hallo delegeren van de server is `connectormachineaccount`. Gebruik deze code als voorbeeld voor Windows 2012 R2:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount mag Hallo SP's-computeraccount of een serviceaccount op welke Hallo SP's groep van toepassingen wordt uitgevoerd.

## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren 
1. Publiceer de toepassing op basis van toohello instructies die worden beschreven [publiceren van toepassingen met toepassingsproxy](application-proxy-publish-azure-portal.md). Zorg ervoor dat tooselect **Azure Active Directory** als Hallo **pre-authenticatie methode**.
2. Nadat uw toepassing wordt weergegeven in de lijst Hallo van zakelijke toepassingen, te selecteren en op **eenmalige aanmelding**.
3. Hallo aanmelding modus voor één te ingesteld**geïntegreerde Windows-verificatie**.  
4. Voer Hallo **interne toepassing SPN** van Hallo-toepassingsserver. In dit voorbeeld is Hallo SPN voor de gepubliceerde toepassing http/www.contoso.com. Deze SPN behoeften toobe in de lijst met services toowhich Hallo Hallo kan gedelegeerde referenties presenteren. 
5. Kies Hallo **overgedragen aanmelding identiteit** voor Hallo connector toouse namens uw gebruikers. Zie voor meer informatie [werken met andere on-premises en cloud-identiteiten](#Working-with-different-on-premises-and-cloud-identities)

   ![Geavanceerde Toepassingsconfiguratie](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Eenmalige aanmelding voor niet-Windows-apps
Hallo stroom van Kerberos-delegering in Azure AD-toepassingsproxy wordt gestart wanneer het Azure AD verifieert de gebruiker Hallo in Hallo cloud. Zodra de aanvraag Hallo lokale aankomt, Hallo hello Azure AD-toepassingsproxy connector een Kerberos-ticket namens de gebruiker Hallo uitgeeft door interactie met lokale Active Directory. Dit proces is waarnaar wordt verwezen tooas Kerberos-beperkt delegatie (KCD). In Hallo volgende fase een aanvraag verzonden toohello back-end-toepassing met dit Kerberos-ticket. Er zijn verschillende protocollen die definiëren hoe de toosend bij dergelijke aanvragen. De meeste niet-Windows-servers verwachten Negotiate/SPNego die nu wordt ondersteund op Azure AD-toepassingsproxy.

Zie voor meer informatie over Kerberos [alle gewenste tooknow over Kerberos-beperkt delegatie (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Niet-Windows-apps doorgaans gebruiker gebruikersnamen of SAM-accountnamen in plaats van domein e-mailadressen. Als deze situatie tooyour toepassingen geldt, moet u tooconfigure Hallo overgedragen aanmelding identiteit veld tooconnect de identiteiten van uw cloud-identiteiten tooyour toepassing. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Werken met andere on-premises en cloud-identiteiten
Toepassingsproxy wordt ervan uitgegaan dat gebruikers exact dezelfde identiteit in Hallo cloud en on-premises Hallo. Als dat niet Hallo geval is, kunt kunt u nog steeds KCD gebruiken voor eenmalige aanmelding. Configureer een **overgedragen aanmelding identiteit** voor elke toepassing toospecify welke identiteit moet worden gebruikt bij het uitvoeren van eenmalige aanmelding.  

Op deze manier kunt veel organisaties die hebben verschillende on-premises en in de cloud identiteiten toohave SSO van hello cloud tooon-premises apps zonder Hallo gebruikers tooenter verschillende gebruikersnamen en wachtwoorden. Dit omvat organisaties die:

* Meerdere domeinen hebt intern (joe@us.contoso.com, joe@eu.contoso.com) en één domein in het Hallo-cloud (joe@contoso.com).
* Niet-routeerbare domeinnaam intern hebt (joe@contoso.usa) en een geldige in Hallo cloud.
* Domeinnamen niet intern gebruiken (Jan)
* Gebruik verschillende aliassen on-premises en in de cloud Hallo. Bijvoorbeeld: joe-johns@contoso.com vs.joej@contoso.com  

Met toepassingsproxy, kunt u selecteren welke identiteit toouse tooobtain Hallo Kerberos-ticket. Deze instelling is per toepassing. Sommige van deze opties zijn geschikt voor systemen die e-mailadres indeling niet accepteert, anderen zijn ontworpen voor alternatieve aanmelding.

![Schermafbeelding van de parameter gedelegeerd aanmelding identiteit](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Als gedelegeerd aanmeldings-id wordt gebruikt, Hallo waarde mogelijk niet uniek zijn in alle Hallo domeinen of forests in uw organisatie. U kunt dit probleem voorkomen door het publiceren van deze toepassingen tweemaal met twee verschillende groepen van Connector. Omdat elke toepassing een andere gebruiker doelgroep heeft, u kunt deelnemen aan het andere domein voor Connectors tooa.

### <a name="configure-sso-for-different-identities"></a>Eenmalige aanmelding configureren voor verschillende identiteiten
1. Azure AD Connect-instellingen configureren zodat hoofdidentiteit Hallo Hallo e-mailadres (e-mail). Dit wordt gedaan deel uit van Hallo proces aanpassen door het wijzigen van Hallo **principalnaam van gebruiker** veld Hallo synchronisatie-instellingen. Deze instellingen bepaalt ook hoe gebruikers zich aanmelden tooOffice365, Windows10 apparaten en andere toepassingen die gebruikmaken van Azure AD als hun identiteit-archief.  
   ![Schermafbeelding van de gebruikers - User Principal Name dropdown identificeren](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. In Hallo Toepassingsconfiguratie-instellingen voor de toepassing hello gewenst toomodify, selecteer Hallo **overgedragen aanmelding identiteit** toobe gebruikt:

   * User Principal Name (bijvoorbeeld joe@contoso.com)
   * Alternatieve UPN-naam (bijvoorbeeld joed@contoso.local)
   * Onderdeel van de gebruikersnaam van de User Principal Name (bijvoorbeeld Jan)
   * Onderdeel van de gebruikersnaam van alternatieve UPN-naam (bijvoorbeeld joed)
   * Lokale SAM-accountnaam (afhankelijk van de configuratie van domeincontroller Hallo)

### <a name="troubleshooting-sso-for-different-identities"></a>Eenmalige aanmelding voor probleemoplossing voor verschillende identiteiten
Als er een fout in Hallo SSO-proces, deze wordt weergegeven in Hallo connector machine gebeurtenislogboek zoals toegelicht in [probleemoplossing](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Maar in sommige gevallen Hallo-aanvraag is verzonden toohello back-end toepassing terwijl deze toepassing in verschillende HTTP-antwoorden beantwoordt. Het oplossen van dergelijke gevallen moet worden gestart door gebeurtenisnummer 24029 op Hallo connector machine in Hallo toepassingsproxy sessie gebeurtenislogboek in. Hallo gebruikers-id die is gebruikt voor overdracht weergegeven in Hallo 'gebruiker' veld binnen de gebeurtenisdetails Hallo. tooturn op sessielogboek, selecteer **logboeken en foutopsporing weergeven analytische** in het menu Hallo event viewer-weergave.

## <a name="next-steps"></a>Volgende stappen

* [Hoe tooconfigure een toepassingsproxy toepassing toouse Kerberos-beperkte overdracht](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Oplossen van problemen met toepassingsproxy](active-directory-application-proxy-troubleshoot.md)


Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)

