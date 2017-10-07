---
title: een Azure line-of-business-app met AD FS-authenticatie aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een line-of-business-app in Azure App Service die met verifieert lokale STS. Deze zelfstudie is bedoeld voor AD FS zoals Hallo lokale STS.
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
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Een Azure line-of-business-app maken met AD FS-verificatie
Dit artikel ziet u hoe toocreate een ASP.NET MVC line-of-business-toepassing in [Azure App Service](../app-service/app-service-value-prop-what-is.md) met behulp van een on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) als Hallo id-provider. Dit scenario kunt werken wanneer u wilt dat toocreate line-of-business-toepassingen in Azure App Service, maar uw organisatie directory gegevens toobe opgeslagen op de locatie vereist.

> [!NOTE]
> Zie voor een overzicht van Hallo verschillende enterprise verificatie en autorisatie opties voor Azure App Service [verifiëren met de lokale Active Directory in uw app in Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Wat u bouwt
Met de volgende kenmerken Hallo bouwt u een eenvoudige ASP.NET-toepassing in Azure App Service Web Apps:

* Verificatie van gebruikers op basis van AD FS
* Maakt gebruik van `[Authorize]` tooauthorize gebruikers voor verschillende acties
* Statische configuratie voor zowel foutopsporing in Visual Studio en publiceren van tooApp Service Web Apps (één keer te configureren, fouten opsporen en op elk gewenst moment publiceren)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Wat u nodig hebt
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

U moet volgen toocomplete Hallo in deze zelfstudie:

* Een on-premises AD FS-implementatie (Zie voor een end-to-end-overzicht van testlab Hallo in deze zelfstudie gebruikt [van het testlab: zelfstandige STS met AD FS in Azure virtuele machine (voor test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Machtigingen toocreate relying party-vertrouwensrelaties in AD FS-beheer
* Visual Studio 2013 Update 4 of hoger
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) of hoger

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Voorbeeld van een toepassing gebruiken voor line-of-business-sjabloon
Voorbeeld van een toepassing in deze zelfstudie Hallo [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), door hello Azure Active Directory-team is gemaakt. Aangezien AD FS WS-Federation ondersteunt, kunt u deze gebruiken als een sjabloon toocreate line-of-business-toepassingen met gemak. Hallo volgende kenmerken heeft:

* Maakt gebruik van [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate met een on-premises AD FS-implementatie
* Functionaliteit voor aanmelden en afmelden
* Maakt gebruik van [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (in plaats van Windows Identity Foundation), die is Hallo toekomstige van ASP.NET en veel eenvoudiger tooset voor verificatie en autorisatie dan WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Hallo-voorbeeldtoepassing instellen
1. Klonen of downloaden Hallo Voorbeeldoplossing op [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour lokale map.
   
   > [!NOTE]
   > instructies op Hallo [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) laten zien hoe u tooset Hallo-toepassing met Azure Active Directory. Maar in deze zelfstudie maakt u instellen met AD FS, dus stappen Hallo hier in plaats daarvan.
   > 
   > 
2. Open Hallo oplossing en open vervolgens Controllers\AccountController.cs in Hallo **Solution Explorer**.
   
   U ziet dat Hallo code gewoon een authentication uitdaging tooauthenticate Hallo-gebruiker met behulp van WS-Federation uitgeeft. Alle verificatie is geconfigureerd in App_Start\Startup.Auth.cs.
3. Open App_Start\Startup.Auth.cs. In Hallo `ConfigureAuth` methode, opmerking Hallo regel:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   In OWIN-wereld Hallo is is in dit fragment in feite Hallo bare dat minimum moet u tooconfigure WS-Federation-verificatie. Het is veel eenvoudiger en meer elegante dan WIF, waarbij Web.config met XML wordt geïnjecteerd over Hallo plaats. Hallo enige informatie die u nodig Hallo van de partij (RP is)-ID en het Hallo-URL van uw AD FS-service-metagegevensbestand. Hier volgt een voorbeeld:
   
   * RP-id:`https://contoso.com/MyLOBApp`
   * Adres van de metagegevens:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. Wijzig in App_Start\Startup.Auth.cs, Hallo statische tekenreeks definities te volgen:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Nu Hallo bijbehorende wijzigingen aanbrengen in het bestand Web.config. Open Web.config Hallo en Hallo volgende app-instellingen wijzigen:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Vul in op basis van uw omgeving respectieve Hallo-sleutelwaarden.
6. Bouw Hallo toepassing toomake ervoor dat er geen fouten zijn.

Dat is alles. Hallo-voorbeeldtoepassing is nu gereed toowork met AD FS. U moet nog steeds tooconfigure een RP-vertrouwensrelatie met deze toepassing in AD FS.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Hallo voorbeeld toepassing tooAzure App Service Web Apps implementeren
Hier kunt publiceren u Hallo toepassing tooa web-app in App Service Web Apps behoud Hallo foutopsporing omgeving. Houd er rekening mee dat u toopublish Hallo toepassing gaat voordat er een RP-vertrouwensrelatie met AD FS, zodat verificatie nog steeds niet nog werkt. Als u deze kunt nu u wel Hallo web app-URL die u later tooconfigure Hallo RP vertrouwensrelatie kunt gebruiken.

1. Met de rechtermuisknop op uw project en selecteer **publiceren**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Selecteer **Microsoft Azure App Service**.
3. Als u dit nog niet hebt aangemeld tooAzure, klikt u op **aanmelden** en Hallo Microsoft-account gebruiken voor uw Azure-abonnement toosign in.
4. Nadat u bent aangemeld, klikt u op **nieuw** toocreate een web-app.
5. Vul alle verplichte velden. U gaat tooconnect tooon-premises gegevens later, zodat een database voor deze web-app niet maken.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Klik op **Create**. Zodra Hallo web-app is gemaakt, wordt Hallo webpublicatie dialoogvenster geopend.
7. In **doel-URL**, wijzigen **http** te**https**. Kopieer Hallo volledige URL tooa teksteditor voor later gebruik. Klik vervolgens op **publiceren**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. Open in Visual Studio **Web.Release.config** in uw project. Invoegen na XML in Hallo Hallo `<configuration>` labelen en Hallo sleutelwaarde vervangen door uw publish web-app-URL.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Wanneer u bent klaar, hebt u twee RP id's die worden geconfigureerd in uw project, één voor uw omgeving voor foutopsporing in Visual Studio en één voor Hallo web-app in Azure hebt gepubliceerd. Stelt u een vertrouwensrelatie RP voor elk van de twee omgevingen Hallo in AD FS. Tijdens de foutopsporing, Hallo app-instellingen in Web.config gebruikte toomake zijn uw **Debug** configuratie werken met AD FS. Wanneer deze wordt gepubliceerd (standaard Hallo **Release** configuratie wordt gepubliceerd), een getransformeerde Web.config waarin Hallo appwijzigingen van de instelling in Web.Release.config wordt geüpload.

Als u wilt dat tooattach Hallo gepubliceerde web-app in Azure toohello foutopsporingsprogramma (dat wil zeggen moet u de symbolen foutopsporing van uw code in Hallo gepubliceerde web-app uploaden), kunt u een kloon van Hallo fouten opsporen in de configuratie voor foutopsporing in Azure, maar met een eigen aangepaste Web.config Transformeren) bijvoorbeeld Web.AzureDebug.config) die gebruikmaakt van app-instellingen van Web.Release.config Hallo. Hiermee kunt u een statische configuratie toomaintain in verschillende omgevingen Hallo.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Vertrouwensrelaties met relying party's in AD FS-beheer configureren
Nu moet u een vertrouwensrelatie RP in AD FS-beheer tooconfigure voordat u kunt uw voorbeeldtoepassing gebruiken en daadwerkelijk met AD FS verifiëren. U moet tooset van twee afzonderlijke RP-vertrouwensrelaties, één voor uw omgeving voor foutopsporing en één voor de gepubliceerde web-app.

> [!NOTE]
> Zorg ervoor dat u de volgende stappen uit voor zowel uw omgevingen Hallo herhaalt.
> 
> 

1. Aanmelden met referenties die tooAD van de rights management FS hebben op uw AD FS-server.
2. Open AD FS-beheer. Met de rechtermuisknop op **AD FS\Trusted Relationships\Relying Party-vertrouwensrelaties** en selecteer **Relying Party Trust toevoegen**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. In Hallo **gegevensbron selecteren** pagina **gegevens over Hallo relying party handmatig invoeren**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. In Hallo **weergavenaam opgeven** pagina, typ een weergavenaam voor de toepassing hello en klikt u op **volgende**.
5. In Hallo **Protocol kiezen** pagina, klikt u op **volgende**.
6. In Hallo **certificaat configureren** pagina, klikt u op **volgende**.
   
   > [!NOTE]
   > Omdat u moet worden gebruikt voor HTTPS al, is versleuteld tokens zijn optioneel. Als u echt tooencrypt tokens van AD FS op deze pagina wilt, moet u ook logica tokenontsleuteling toevoegen in uw code. Zie voor meer informatie [handmatig OWIN WS-Federation-middleware configureren en het accepteren van tokens versleuteld](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Voordat u naar de volgende stap hello verplaatst, moet u een stukje informatie van uw Visual Studio-project. In de Projecteigenschappen hello, houd er rekening mee Hallo **SSL URL** van Hallo-toepassing. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. Terug in AD FS-beheer in Hallo **URL configureren** pagina Hallo **toevoegen Wizard Relying Party Trust**, selecteer **ondersteuning voor Hallo WS-Federation Passive protocol inschakelen** en Typ in Hallo SSL-URL van uw Visual Studio-project dat u hebt genoteerd in de vorige stap Hallo. Klik op **Volgende**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL bevat waar toosend Hallo client na verificatie is geslaagd. Hallo foutopsporing omgeving moet <code>https://localhost:&lt;port&gt;/</code>. Voor Hallo gepubliceerde web-app moet het Hallo web-app-URL.
   > 
   > 
9. In Hallo **id's configureren** pagina, controleert u of de SSL-URL van uw project al is vermeld en klik op **volgende**. Klik op **volgende** alle Hallo manier toohello einde van de standaardselecties Hallo-wizard.
   
   > [!NOTE]
   > In App_Start\Startup.Auth.cs van Visual Studio-project deze id wordt vergeleken met de waarde van Hallo <code>WsFederationAuthenticationOptions.Wtrealm</code> tijdens federatieve verificatie. Standaard wordt van de toepassing hello-URL van de vorige stap Hallo toegevoegd als een RP-id.
   > 
   > 
10. U bent nu klaar Hallo RP-toepassing voor uw project in AD FS configureren. Vervolgens configureert u deze toepassing toosend Hallo claims die nodig is voor uw toepassing. Hallo **Claimregels bewerken** dialoogvenster wordt standaard voor u geopend aan einde van de wizard Hallo Hallo zodat u meteen kunt gaan. We gaan configureren ten minste Hallo volgende claims (met schema's tussen haakjes):
    
    * Naam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - gebruikt door ASP.NET toohydrate `User.Identity.Name`.
    * Gebruiker (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - UPN gebruikt toouniquely Identificeer gebruikers in het Hallo-organisatie.
    * Groepslidmaatschappen als (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - rollen kan worden gebruikt met `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize domeincontrollers/acties. In werkelijkheid is kan deze methode niet worden Hallo meeste zodat voor rolautorisatie. Als uw AD-gebruikers toohundreds van beveiligingsgroepen behoren, worden ze honderden rolclaims in Hallo SAML-token. Een alternatieve methode is toosend één rol claim voorwaardelijk afhankelijk van Hallo gebruiker lid is van een bepaalde groep. Maar je we Houd het eenvoudig voor deze zelfstudie.
    * Gebruikersnaam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - kunnen worden gebruikt voor validatie antivirusprogramma kunnen worden vervalst. Zie voor meer informatie over hoe de toomake is werken met ter voorkoming validatie, Hallo **line-of-business-functionaliteit toevoegen** sectie van [een Azure line-of-business-app maken met Azure Active Directory-verificatie ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Hallo claim typt u tooconfigure nodig hebt voor uw toepassing wordt bepaald door de behoeften van uw toepassing. Hallo-lijst met claims die worden ondersteund door Azure Active Directory-toepassingen (dat wil zeggen RP-vertrouwensrelaties), bijvoorbeeld zien [ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. Klik in het dialoogvenster Claimregels bewerken Hallo **regel toevoegen**.
12. Hallo-naam, UPN en rol claims configureren, zoals weergegeven in de schermafbeelding Hallo en klik op **voltooien**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Maak vervolgens een tijdelijke naam ID claim in met behulp van Hallo stappen uitgelegd [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Klik op **regel toevoegen** opnieuw.
14. Selecteer **Claims verzenden met een aangepaste regel** en klik op **volgende**.
15. Plakken Hallo volgende regel taal in Hallo **aangepaste regel** vak, naam Hallo regel **Per sessie-id** en klik op **voltooien**.  
    
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
18. Hallo regel configureren, zoals weergegeven in Hallo schermafbeelding (met claimtype Hallo u hebt gemaakt in een aangepaste regel Hallo) en klik op **voltooien**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Zie voor gedetailleerde informatie over Hallo stappen voor het Hallo tijdelijke naam-ID claim [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Klik op **toepassen** in Hallo **Claimregels bewerken** dialoogvenster. Deze ziet er nu als Hallo schermafbeelding te volgen:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Zorg ervoor dat u deze stappen herhalen voor uw omgeving voor foutopsporing en de gepubliceerde web-app.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Federatieve verificatie voor uw toepassing testen
U bent gereed tootest verificatielogica van uw toepassing op basis van AD FS. Ik heb een testgebruiker die deel uitmaakt van tooa testgroep in Active Directory (AD) in de AD FS-testomgeving.

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

tootest verificatie in Hallo foutopsporingsprogramma, hoeft u toodo nu is type `F5`. Als u tootest verificatie in Hallo gepubliceerde web-app wilt, navigeer toohello URL.

Nadat het Hallo-webtoepassing is geladen, klikt u op **aanmelden**. Nu moet u ofwel een dialoogvenster of Hallo aanmelding aanmeldingspagina afgehandeld door AD FS is afhankelijk van de verificatiemethode Hallo gekozen door AD FS. Hier volgt ik in Internet Explorer 11 krijgen.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Zodra u aanmelden als gebruiker in Hallo AD-domein van Hallo AD FS-implementatie, u ziet nu Hallo startpagina opnieuw met **Hello, <User Name>!** Hallo klikken in. Hier volgt krijg ik.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

U hebt tot nu toe is voltooid in de volgende manieren Hallo:

* Uw toepassing heeft de AD FS is bereikt en een overeenkomende RP-id is gevonden in Hallo AD FS-database
* AD FS is geverifieerd een AD-gebruiker en u een back-startpagina van de toepassing toohello-omleiding
* AD FS als de naam van de verzonden hello claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour toepassing, zoals aangegeven door Hallo feit die gebruiker Hallo naam wordt weergegeven in Hallo hoek. 

Als de naamclaim Hallo ontbreekt, u zou hebben gezien **Hello,!**. Als u Views\Shared bekijkt\_LoginPartial.cshtml, vindt u die gebruikmaakt van `User.Identity.Name` toodisplay Hallo-gebruikersnaam. Zoals eerder vermeld als Hallo naam claim Hallo geverifieerde gebruiker is beschikbaar in Hallo SAML-token, hydrates ASP.NET deze eigenschap aan. alle Hallo toosee claims worden verzonden door AD FS, een onderbrekingspunt in Controllers\HomeController.cs, plaatsen in de Hallo Index actiemethode. Nadat het Hallo-gebruiker is geverifieerd, inspecteren Hallo `System.Security.Claims.Current.Claims` verzameling.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autoriseren van gebruikers voor specifieke domeincontrollers of acties
Aangezien u groepslidmaatschappen als rolclaims in uw configuratie van de vertrouwensrelatie RP hebt opgenomen, kunt u nu gebruiken ze rechtstreeks in Hallo `[Authorize(Roles="...")]` decoration voor domeincontrollers en acties. In een line-of-business-toepassing met Hallo maken, lezen, bijwerken, verwijderen (CRUD) patroon, kunt u specifieke rollen tooaccess elke actie autoriseren. Op dit moment wordt u alleen deze functie op Hallo bestaande Home domeincontroller uitproberen.

1. Open Controllers\HomeController.cs.
2. Hallo opmaken `About` en `Contact` actie methoden vergelijkbaar toohello de volgende code, met behulp van de geverifieerde gebruiker heeft beveiligingsgroepen.  
   
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
   
    Nadat ik toegevoegd **testgebruiker** te**testgroep** in mijn AD FS-testomgeving ik testgroep tootest autorisatie gebruik op `About`. Voor `Contact`, test ik Hallo negatieve geval van **Domeinadministrators**, toowhich **gebruiker testen** behoort niet toe.
3. Hallo-foutopsporingsprogramma start door te typen `F5` en meld u aan en klik vervolgens op **over**. U moet nu worden bekijkt hello `~/About/Index` pagina geslaagd, als de geverifieerde gebruiker is gemachtigd voor deze actie.
4. Klik nu op **Contact**, die in mijn geval dienen niet toe te staan **testgebruiker** voor Hallo actie. Hallo browser is echter omgeleide tooAD FS, die uiteindelijk ziet u dit bericht:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Als u deze fout in Logboeken op Hallo AD FS-server onderzoeken, ziet u dit bericht van uitzondering:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Hallo reden voor deze fout is dat standaard MVC retourneert een 401 niet geautoriseerd wanneer rollen van een gebruiker bent niet gemachtigd. Dit activeert een herauthenticatie aanvraag tooyour id-provider (AD FS). Aangezien het Hallo-gebruiker is al geverifieerd, AD FS toohello retourneert dezelfde pagina die u vervolgens een andere 401 verstrekt, een lus omleiding maken. Overschrijft u de AuthorizeAttribute `HandleUnauthorizedRequest` methode met een eenvoudige logische tooshow iets wat zinvol in plaats van de bewerking wordt voortgezet Hallo omleidings-lus.
5. Maak een bestand in Hallo project met de naam AuthorizeAttribute.cs en plakken Hallo code in het volgende.
   
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
   
    Hallo code verzendt een HTTP 403 (verboden) in plaats van 401 HTTP-(niet-geautoriseerd) in geverifieerde maar niet-geautoriseerde gevallen overschrijven.
6. Voer Hallo foutopsporingsprogramma opnieuw met `F5`. Te klikken op **Contact** nu een meer informatieve (die mogelijk zwartwitprinter) foutbericht weergegeven:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Hallo toepassing tooAzure App Service Web Apps opnieuw publiceren en te testen Hallo gedrag van Hallo live-toepassing.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Verbinding maken met tooon lokale gegevens
Een reden is dat u tooimplement uw line-of-business-toepassing met AD FS in plaats van Azure Active Directory wilt problemen met de compatibiliteit met het up-to-date houden organisatie gegevens uit de lokale. Dit kan ook betekenen dat uw web-app in Azure toegang lokale databases, tot moet omdat het is niet toegestaan toouse [SQL-Database](/services/sql-database/) als gegevenslaag Hallo voor uw web-apps.

Azure App Service Web Apps biedt ondersteuning voor toegang tot lokale databases met twee benaderingen: [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [virtuele netwerken](web-sites-integrate-with-vnet.md). Zie voor meer informatie [VNET met behulp van integratie en hybride verbindingen met Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Meer bronnen
* [Verificatie met de on-premises Active Directory in uw app in Azure](web-sites-authentication-authorization.md)
* [Een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md)
* [Gebruik Hallo On-Premises organisatie verificatie optie (ADFS) met ASP.NET in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Een tooKatana VS2013 Web Project van WIF migreren](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Overzicht van Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)
* [1.1 van WS-Federation-specificatie](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

