---
title: Een Azure line-of-business-app maken met AD FS-verificatie | Microsoft Docs
description: Informatie over het maken van een line-of-business-app in Azure App Service die wordt geverifieerd met lokale STS. Deze zelfstudie is bedoeld voor AD FS als de lokale STS.
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Een Azure line-of-business-app maken met AD FS-verificatie
Dit artikel ziet u het maken van een ASP.NET MVC-line-of-business-toepassing in [Azure App Service](../app-service/app-service-value-prop-what-is.md) met behulp van een on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) als de id-provider. Dit scenario kunt werken wanneer u wilt maken van line-of-business-toepassingen in Azure App Service, maar uw organisatie vereist dat directorygegevens op de locatie worden opgeslagen.

> [!NOTE]
> Zie voor een overzicht van de andere enterprise-verificatie en autorisatie opties voor Azure App Service [verifiëren met de lokale Active Directory in uw app in Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Wat u bouwt
Maakt u een eenvoudige ASP.NET-toepassing in Azure App Service Web Apps met de volgende functies:

* Verificatie van gebruikers op basis van AD FS
* Maakt gebruik van `[Authorize]` voor het autoriseren van gebruikers voor verschillende acties
* Statische configuratie voor zowel foutopsporing in Visual Studio en publiceren naar App Service Web Apps (één keer te configureren, fouten opsporen en op elk gewenst moment publiceren)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Wat u nodig hebt
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

U moet het volgende om deze zelfstudie te voltooien:

* Een on-premises AD FS-implementatie (Zie voor een end-to-end-overzicht van het testlab in deze zelfstudie gebruikt [van het testlab: zelfstandige STS met AD FS in Azure virtuele machine (voor test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Machtigingen voor het maken van de relying partij vertrouwensrelaties in AD FS-beheer
* Visual Studio 2013 Update 4 of hoger
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) of hoger

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Voorbeeld van een toepassing gebruiken voor line-of-business-sjabloon
De voorbeeldtoepassing in deze zelfstudie [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is gemaakt door het team van Azure Active Directory. Aangezien AD FS WS-Federation ondersteunt, kunt u deze als sjabloon gebruiken line-of-business-toepassingen maken met gemak. Het bevat de volgende functies:

* Maakt gebruik van [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) voor verificatie met een on-premises AD FS-implementatie
* Functionaliteit voor aanmelden en afmelden
* Maakt gebruik van [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (in plaats van Windows Identity Foundation), dat wil zeggen de toekomstige van ASP.NET en veel eenvoudiger om in te stellen voor verificatie en autorisatie dan WIF

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a>Instellen van de voorbeeldtoepassing
1. Klonen of downloaden van de Voorbeeldoplossing in [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) naar uw lokale map.
   
   > [!NOTE]
   > De instructies op de [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) beschreven hoe u met het instellen van de toepassing met Azure Active Directory. Maar in deze zelfstudie maakt u instellen met AD FS, volg daarom de volgende stappen uit in plaats daarvan.
   > 
   > 
2. Open de oplossing en open vervolgens Controllers\AccountController.cs in de **Solution Explorer**.
   
   U ziet dat de code gewoon een verificatiecontrole voor het verifiëren met behulp van WS-Federation uitgeeft. Alle verificatie is geconfigureerd in App_Start\Startup.Auth.cs.
3. Open App_Start\Startup.Auth.cs. In de `ConfigureAuth` methode, Let op de regel:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   In de wereld OWIN is in dit fragment in feite minimaal moet u WS-Federation-verificatie configureren. Het is veel eenvoudiger en meer elegante dan WIF, waarbij Web.config met XML is ingevoegd in de plaats. De enige informatie die u nodig is de relying party van (RP)-ID en de URL van het metagegevensbestand van uw AD FS-service. Hier volgt een voorbeeld:
   
   * RP-id:`https://contoso.com/MyLOBApp`
   * Adres van de metagegevens:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. Op App_Start\Startup.Auth.cs, wijzigt u de volgende definities van de vaste tekenreeks:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Nu de bijbehorende wijzigingen aanbrengen in het bestand Web.config. Open het bestand Web.config en de volgende appinstellingen wijzigen:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Vul in de sleutelwaarden op basis van de respectieve omgeving.
6. Maken van de toepassing om te controleren of dat er zijn geen fouten.

Dat is alles. De voorbeeldtoepassing is nu gereed voor gebruik met AD FS. U moet nog steeds een vertrouwensrelatie RP met deze toepassing in AD FS configureren.

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a>De voorbeeldtoepassing op Azure App Service Web Apps implementeren
Hier kunt publiceren u de toepassing naar een web-app in App Service Web Apps behoud de foutopsporing-omgeving. Houd er rekening mee dat u gaat de toepassing publiceren voordat er een RP-vertrouwensrelatie met AD FS, zodat verificatie nog steeds niet nog werkt. Als u deze kunt nu u wel de app-URL die u gebruiken kunt voor het configureren van de vertrouwensrelatie RP later.

1. Met de rechtermuisknop op uw project en selecteer **publiceren**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Selecteer **Microsoft Azure App Service**.
3. Als u dit nog niet hebt aangemeld bij Azure, klikt u op **aanmelden** en gebruiken van het Microsoft-account voor uw Azure-abonnement aan te melden.
4. Nadat u bent aangemeld, klikt u op **nieuw** voor het maken van een web-app.
5. Vul alle verplichte velden. U wilt verbinding maken met on-premises gegevens later, zodat een database voor deze web-app niet maken.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Klik op **Create**. Zodra de web-app is gemaakt, wordt het dialoogvenster Publish Web geopend.
7. In **doel-URL**, wijzigen **http** naar **https**. Kopieer de volledige URL naar een teksteditor voor later gebruik. Klik vervolgens op **publiceren**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Open in Visual Studio **Web.Release.config** in uw project. Voeg de volgende XML in de `<configuration>` labelen en vervang de waarde van de sleutel met uw publish web-app-URL.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Wanneer u bent klaar, hebt u twee RP id's die worden geconfigureerd in uw project, één voor uw omgeving voor foutopsporing in Visual Studio en één voor de gepubliceerde web-app in Azure. Stelt u een vertrouwensrelatie RP voor elk van deze twee omgevingen in AD FS. Tijdens de foutopsporing, instellingen voor de app in web.config-bestand worden gebruikt om uw **Debug** configuratie werken met AD FS. Wanneer deze wordt gepubliceerd (standaard de **Release** configuratie wordt gepubliceerd), een getransformeerde Web.config waarin de wijzigingen van de app-instelling in Web.Release.config wordt geüpload.

Als u wilt koppelen van de gepubliceerde web-app in Azure om het foutopsporingsprogramma (dat wil zeggen moet u de symbolen foutopsporing van uw code in de gepubliceerde web-app uploaden), kunt u een kloon van de configuratie van de foutopsporing voor het opsporen van Azure, maar met een eigen aangepaste Web.config-transformatie (bijvoorbeeld Web.AzureDebug.config) die gebruikmaakt van de appinstellingen van Web.Release.config maken. Hiermee kunt u de configuratie van een statische onderhouden in de verschillende omgevingen.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Vertrouwensrelaties met relying party's in AD FS-beheer configureren
Nu moet u een vertrouwensrelatie RP in AD FS-beheer configureren voordat u kunt de voorbeeldtoepassing en daadwerkelijk met AD FS verifiëren. U moet twee afzonderlijke RP-vertrouwensrelaties, één voor uw omgeving voor foutopsporing en één voor de gepubliceerde web-app instellen.

> [!NOTE]
> Zorg ervoor dat u de volgende stappen herhalen voor zowel uw omgevingen.
> 
> 

1. Aanmelden met referenties op waarmee de rights management in AD FS hebt op uw AD FS-server.
2. Open AD FS-beheer. Met de rechtermuisknop op **AD FS\Trusted Relationships\Relying Party-vertrouwensrelaties** en selecteer **Relying Party Trust toevoegen**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. In de **gegevensbron selecteren** pagina **gegevens over de relying party handmatig invoeren**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. In de **weergavenaam opgeven** pagina, typ een weergavenaam voor de toepassing en klik op **volgende**.
5. In de **Protocol kiezen** pagina, klikt u op **volgende**.
6. In de **certificaat configureren** pagina, klikt u op **volgende**.
   
   > [!NOTE]
   > Omdat u moet worden gebruikt voor HTTPS al, is versleuteld tokens zijn optioneel. Als u zeker versleutelen tokens van AD FS op deze pagina wilt, moet u ook logica tokenontsleuteling toevoegen in uw code. Zie voor meer informatie [handmatig OWIN WS-Federation-middleware configureren en het accepteren van tokens versleuteld](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Voordat u naar de volgende stap verplaatst, moet u een stukje informatie van uw Visual Studio-project. Noteer in de Projecteigenschappen de **SSL URL** van de toepassing. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. AD FS-beheer, weer de **URL configureren** pagina van de **toevoegen Wizard Relying Party Trust**, selecteer **ondersteuning voor de WS-Federation Passive protocol inschakelen** en typt u de SSL-URL van uw Visual Studio-project dat u in de vorige stap hebt genoteerd. Klik op **Volgende**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL geeft aan waar de client verzenden nadat een verificatie geslaagde. Voor de omgeving foutopsporing moet <code>https://localhost:&lt;port&gt;/</code>. Voor de gepubliceerde web-app, moet de app-URL.
   > 
   > 
9. In de **id's configureren** pagina, controleert u of de SSL-URL van uw project al is vermeld en klik op **volgende**. Klik op **volgende** helemaal tot aan het einde van de wizard met de standaardselecties.
   
   > [!NOTE]
   > In App_Start\Startup.Auth.cs van Visual Studio-project deze id wordt vergeleken met de waarde van <code>WsFederationAuthenticationOptions.Wtrealm</code> tijdens federatieve verificatie. Standaard wordt de URL van de toepassing van de vorige stap toegevoegd als een RP-id.
   > 
   > 
10. U bent nu klaar om de RP-toepassingen configureren voor uw project in AD FS. Vervolgens configureert u deze toepassing verzenden van de claims die nodig is voor uw toepassing. De **Claimregels bewerken** dialoogvenster wordt standaard voor u geopend aan het einde van de wizard zodat u meteen kunt gaan. Laten we Configureer ten minste de volgende claims (met schema's tussen haakjes):
    
    * Naam van (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - door ASP.NET hydrate `User.Identity.Name`.
    * UPN (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn -) gebruikt als unieke identificatie van gebruikers in de organisatie.
    * Groepslidmaatschappen als (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - rollen kan worden gebruikt met `[Authorize(Roles="role1, role2,...")]` decoration domeincontrollers/acties autoriseren. Deze aanpak mogelijk in werkelijkheid is niet de meeste zodat voor rolautorisatie. Als uw AD-gebruikers tot honderden beveiligingsgroepen behoren, worden ze honderden rolclaims in het SAML-token. Er is een alternatieve methode voor het verzenden van een claim één rol voor voorwaardelijk afhankelijk van het lidmaatschap van de gebruiker in een bepaalde groep. Maar je we Houd het eenvoudig voor deze zelfstudie.
    * Gebruikersnaam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - kunnen worden gebruikt voor validatie antivirusprogramma kunnen worden vervalst. Zie voor meer informatie over het maken van werken met ter voorkoming validatie de **line-of-business-functionaliteit toevoegen** sectie van [een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > De claimtypen die u wilt configureren voor uw toepassing wordt bepaald door de behoeften van uw toepassing. Voor de lijst met claims die worden ondersteund door Azure Active Directory-toepassingen (dat wil zeggen RP-vertrouwensrelaties), bijvoorbeeld zien [ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Klik in het dialoogvenster Claimregels bewerken op **regel toevoegen**.
12. De naam, UPN en rol claims configureren zoals wordt weergegeven in de schermafbeelding en klik op **voltooien**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Maak vervolgens een tijdelijke naam ID claim in met behulp van de stappen uitgelegd [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Klik op **regel toevoegen** opnieuw.
14. Selecteer **Claims verzenden met een aangepaste regel** en klik op **volgende**.
15. Plak de volgende regel taal in de **aangepaste regel** vak en de naam van de regel **Per sessie-id** en klik op **voltooien**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    Uw aangepaste regel moet eruitzien als in deze schermafbeelding:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Klik op **regel toevoegen** opnieuw.
17. Selecteer **een binnenkomende Claim transformeren** en klik op **volgende**.
18. De regel configureren zoals wordt weergegeven in de schermafbeelding (met het claimtype die u hebt gemaakt in de aangepaste regel) en klik op **voltooien**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Zie voor gedetailleerde informatie over de stappen voor de tijdelijke naam-ID claim [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Klik op **toepassen** in de **Claimregels bewerken** dialoogvenster. Nu ziet er in de volgende schermafbeelding:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Zorg ervoor dat u deze stappen herhalen voor uw omgeving voor foutopsporing en de gepubliceerde web-app.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Federatieve verificatie voor uw toepassing testen
U bent klaar voor het testen van uw toepassing verificatielogica op basis van AD FS. Ik heb een testgebruiker op die bij een testgroep in Active Directory (AD hoort) in de AD FS-testomgeving.

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

Als u wilt testen verificatie in het foutopsporingsprogramma, hoeft u nu type is `F5`. Als u testen verificatie in de gepubliceerde web-app wilt, gaat u naar de URL.

Nadat de webtoepassing is geladen, klikt u op **aanmelden**. U krijgt nu een dialoogvenster voor aanmelding of de aanmeldingspagina afgehandeld door AD FS is afhankelijk van de verificatiemethode die wordt gekozen door AD FS. Hier volgt ik in Internet Explorer 11 krijgen.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Zodra u aanmelden als gebruiker in het AD-domein van de AD FS-implementatie, u ziet nu de startpagina opnieuw met **Hello, <User Name>!** in de hoek. Hier volgt krijg ik.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

U hebt tot nu toe is voltooid op de volgende manieren:

* Uw toepassing heeft de AD FS is bereikt en een overeenkomende RP-id is gevonden in de AD FS-database
* AD FS is geverifieerd een AD-gebruiker en een omleiding die u terug naar de startpagina van de toepassing
* AD FS als verzonden de naamclaim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) voor uw toepassing, zoals aangegeven door het feit dat de gebruikersnaam wordt weergegeven in de hoek. 

Als de claim ontbreekt, u zou hebben gezien **Hello,!**. Als u Views\Shared bekijkt\_LoginPartial.cshtml, vindt u die gebruikmaakt van `User.Identity.Name` om de naam van de gebruiker weer te geven. Zoals gezegd, als de naamclaim van de geverifieerde gebruiker beschikbaar in het SAML-token is, hydrates ASP.NET deze eigenschap aan. Overzicht van de claims die worden verzonden door AD FS een onderbrekingspunt in Controllers\HomeController.cs, te plaatsen in de Index-actiemethode. Nadat de gebruiker is geverifieerd, Inspecteer de `System.Security.Claims.Current.Claims` verzameling.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autoriseren van gebruikers voor specifieke domeincontrollers of acties
Aangezien u groepslidmaatschappen als rolclaims in uw configuratie van de vertrouwensrelatie RP hebt opgenomen, kunt u nu gebruiken ze rechtstreeks in de `[Authorize(Roles="...")]` decoration voor domeincontrollers en acties. U kunt specifieke functies voor toegang tot elke actie autoriseren in een line-of-business-toepassing met het patroon maken, lezen, bijwerken, verwijderen (CRUD). Op dit moment wordt u alleen deze functie op de bestaande Home controller uitproberen.

1. Open Controllers\HomeController.cs.
2. Opmaken de `About` en `Contact` actiemethoden vergelijkbaar met de volgende code, met security groepslidmaatschappen dat de geverifieerde gebruiker heeft.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Nadat ik toegevoegd **gebruiker testen** naar **testgroep** in mijn AD FS-testomgeving ik testgroep gebruik autorisatie testen op `About`. Voor `Contact`, test ik het negatieve geval van **Domeinadministrators**toe aan die **gebruiker testen** behoort niet toe.
3. Het foutopsporingsprogramma start door te typen `F5` en meld u aan en klik vervolgens op **over**. U moet nu bekijkt de `~/About/Index` pagina geslaagd, als de geverifieerde gebruiker is gemachtigd voor deze actie.
4. Klik nu op **Contact**, die in mijn geval dienen niet toe te staan **testgebruiker** voor de actie. Echter, de browser wordt omgeleid naar AD FS, die uiteindelijk ziet u dit bericht:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Als u deze fout in Logboeken op de AD FS-server onderzoeken, ziet u dit bericht van uitzondering:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    De reden voor deze fout is dat standaard MVC een 401 niet geautoriseerd retourneert wanneer rollen van een gebruiker bent niet gemachtigd. Dit activeert een aanvraag herauthenticatie id-provider (AD FS). Omdat de gebruiker al is geverifieerd, wordt AD FS retourneert op dezelfde pagina, vervolgens geeft u een andere 401, een lus omleiding maken. Overschrijft u de AuthorizeAttribute `HandleUnauthorizedRequest` methode met eenvoudige logica voor het weergeven van iets die zinvol in plaats van de lus omleiding u doorgaat.
5. Maak een bestand in het project met de naam AuthorizeAttribute.cs en plak de volgende code in deze.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    De onderdrukking code verzendt een HTTP 403 (verboden) in plaats van 401 HTTP-(niet-geautoriseerd) in geverifieerde maar niet-geautoriseerde gevallen.
6. Voer het foutopsporingsprogramma opnieuw met `F5`. Te klikken op **Contact** nu een meer informatieve (die mogelijk zwartwitprinter) foutbericht weergegeven:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. De toepassing publiceren in Azure App Service Web Apps opnieuw en het gedrag van de live-toepassing te testen.

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a>Verbinding maken met on-premises gegevens
Een reden zou willen implementeren van uw line-of-business-toepassing met AD FS in plaats van Azure Active Directory is problemen met de compatibiliteit met het up-to-date houden organisatie gegevens uit de lokale. Dit kan ook betekenen dat uw web-app in Azure toegang lokale databases, tot moet omdat u niet mag gebruiken [SQL-Database](/services/sql-database/) als de gegevenslaag voor uw web-apps.

Azure App Service Web Apps biedt ondersteuning voor toegang tot lokale databases met twee benaderingen: [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [virtuele netwerken](web-sites-integrate-with-vnet.md). Zie voor meer informatie [VNET met behulp van integratie en hybride verbindingen met Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Meer bronnen
* [Verificatie met de on-premises Active Directory in uw app in Azure](web-sites-authentication-authorization.md)
* [Een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md)
* [De optie voor organisatie-verificatie in de On-Premises (AD FS) gebruiken met ASP.NET in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Migreren van een webproject VS2013 van WIF naar Katana](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Overzicht van Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)
* [1.1 van WS-Federation-specificatie](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

