---
title: Systeem voor het identiteitsbeheer tussen domeinen aaaUsing automatisch worden ingericht, gebruikers en groepen van Azure Active Directory-tooapplications | Microsoft Docs
description: Azure Active Directory kunnen automatisch worden ingericht, gebruikers en groepen tooany toepassing of identiteit store, die door een webservice is fronted met Hallo interface is gedefinieerd in Hallo SCIM protocol specification
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Met behulp van systeem voor identiteitsbeheer van verschillende domeinen tooautomatically inrichten gebruikers en groepen van Azure Active Directory-tooapplications

## <a name="overview"></a>Overzicht
Azure Active Directory (Azure AD) kunnen automatisch worden ingericht, gebruikers en groepen tooany toepassing of identiteit store, die door een webservice met gedefinieerd in Hallo Hallo-interface is fronted [systeem voor verschillende domeinen Identity Management (SCIM) 2.0 Protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory kunt verzenden aanvragen toocreate, wijzigen of verwijderen van toegewezen gebruikers en groepen toohello webservice. Hallo-webservice kan vervolgens deze aanvragen worden omgezet in bewerkingen op Hallo doel identiteit store. 

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. 



![][0]
*Afbeelding 1: Inrichting van Azure Active Directory tooan identiteit store via een webservice*

Deze mogelijkheid kan worden gebruikt in combinatie met 'bring your own app' Hallo-functionaliteit in Azure AD tooenable eenmalige aanmelding en automatisch gebruikers inrichten voor toepassingen die op of door een webservice SCIM zijn fronted.

Er zijn twee gebruiksvoorbeelden voor using SCIM in Azure Active Directory:

* **Inrichting van gebruikers en groepen tooapplications die ondersteuning bieden voor SCIM** toepassingen die ondersteuning bieden voor SCIM 2.0 en bearer-tokens van OAuth gebruiken voor verificatie met Azure AD zonder configuratie werkt.
* **Maak uw eigen inrichting oplossing voor toepassingen die ondersteuning bieden voor andere inrichting op basis van een API** voor niet-SCIM toepassingen, kunt u een SCIM eindpunt tootranslate tussen hello Azure AD SCIM eindpunt en elke API Hallo toepassing ondersteunt maken voor gebruikers inrichten. toohelp u een eindpunt SCIM ontwikkelen, bieden we Common Language Infrastructure (CLI)-bibliotheken en codevoorbeelden waarin wordt uitgelegd hoe toodo bieden een eindpunt SCIM en SCIM berichten vertalen.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Gebruikers en groepen tooapplications die ondersteuning bieden voor SCIM inrichten
Azure AD kan worden geconfigureerd tooautomatically inrichten toegewezen gebruikers en groepen tooapplications die implementeren een [systeem voor verschillende domeinen Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) webservice en accepteren OAuth bearer-tokens voor authenticatie . Toepassingen moeten voldoen aan deze vereisten binnen Hallo SCIM 2.0-specificatie:

* Ondersteunt het maken van gebruikers en/of groepen aan de hand van sectie 3.3 Hallo SCIM-protocol.  
* Ondersteunt het wijzigen van gebruikers en/of groepen met patch-aanvragen aan de hand van sectie 3.5.2 Hallo SCIM-protocol.  
* Ondersteunt het ophalen van een bekende bron volgens punt 3.4.1 Hallo SCIM-protocol.  
* Ondersteunt het opvragen van gebruikers en/of groepen aan de hand van sectie 3.4.2 Hallo SCIM-protocol.  Standaard door externalId aan gebruikers gevraagd en groepen worden opgevraagd met de weergavenaam.  
* Ondersteunt het opvragen van de gebruiker door-ID en -beheer volgens sectie 3.4.2 Hallo SCIM-protocol.  
* Ondersteunt het uitvoeren van query's groepen door-ID en door een lid aan de hand van sectie 3.4.2 Hallo SCIM-protocol.  
* OAuth-bearer-tokens voor autorisatie volgens punt 2.1 Hallo SCIM protocol accepteert.

Neem contact op met uw toepassingsprovider of de documentatie van uw toepassingsprovider voor overzichten van compatibiliteit met deze vereisten.

### <a name="getting-started"></a>Aan de slag
Toepassingen die ondersteuning bieden voor Hallo SCIM profiel dat wordt beschreven in dit artikel kunnen worden verbonden tooAzure Active Directory Hallo 'niet galerie application' gebruiken in hello Azure AD-toepassingsgalerie. Zodra de verbonden, Azure AD wordt uitgevoerd een synchronisatieproces om de 20 minuten waar query uit te voeren van de toepassing hello SCIM eindpunt voor toegewezen gebruikers en groepen uit en maakt of wijzigt volgens toohello Toewijzingsdetails.

**een toepassing die ondersteuning biedt voor SCIM tooconnect:**

1. Aanmelden te[hello Azure-portal](https://portal.azure.com). 
2. Te bladeren ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.
3. Voer een naam voor uw toepassing en klik op **toevoegen** pictogram toocreate een app-object.
    
  ![][1]
  *Afbeelding 2: Azure AD-toepassingsgalerie*
    
4. Selecteer in de resulterende welkomstscherm Hallo **inrichten** tabblad in de linkerkolom Hallo.
5. In Hallo **modus inrichting** selecteert u **automatische**.
    
  ![][2]
  *Afbeelding 3: Configureren in Azure-portal Hallo inrichting*
    
6. In Hallo **Tenant-URL** Voer Hallo-URL van de van toepassing hello SCIM eindpunt. Voorbeeld: https://api.contoso.com/scim/v2/
7. Als Hallo SCIM eindpunt een OAuth bearer-token van een verlener dan Azure AD vereist, wordt de kopie Hallo OAuth bearer-token in Hallo optionele vereist **geheim Token** veld. Als dit veld leeg blijft, opgenomen een OAuth-bearer-token uitgegeven vanuit Azure AD bij elke aanvraag met Azure AD. Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.
8. Klik op Hallo **testverbinding** knop toohave Azure Active Directory poging tooconnect toohello SCIM eindpunt. Als Hallo pogingen mislukken, wordt informatie over de fout wordt weergegeven.  
9. Als Hallo pogingen tooconnect toohello toepassing slaagt, klikt u op **opslaan** toosave Hallo beheerdersreferenties.
10. In Hallo **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten. Selecteer elke één tooreview Hallo kenmerken die worden gesynchroniseerd vanuit Azure Active Directory tooyour app. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikers en groepen in uw app voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.

    >[!NOTE]
    >U kunt desgewenst uitschakelen door Hallo 'groepen' toewijzing uit te schakelen van een groepsobjecten worden gesynchroniseerd. 

11. Onder **instellingen**, Hallo **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd. Alleen selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) worden gesynchroniseerd gebruikers en groepen die zijn toegewezen in Hallo **gebruikers en groepen** tabblad.
12. Zodra de configuratie voltooid is, verandert Hallo **inrichting Status** te**op**.
13. Klik op **opslaan** toostart Hallo inrichting Azure AD-service. 
14. Als alleen synchroniseren toegewezen gebruikers en groepen (aanbevolen), moet u ervoor tooselect Hallo **gebruikers en groepen** tabblad en Hallo-gebruikers en/of groepen die u wenst dat toosync toewijzen.

Nadat de initiële synchronisatie Hallo is gestart, kunt u Hallo **controlelogboeken** tabblad toomonitor voortgang, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app wordt ingericht. Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Uw eigen oplossing voor elke toepassing bouwen
Als u een SCIM-webservice die is gekoppeld met Azure Active Directory maakt, kunt u één gebruiker voor eenmalige aanmelding en automatische inrichting voor vrijwel elke toepassing die voorziet in een API-inrichting REST of SOAP-gebruiker.

Hier ziet u hoe het werkt:

1. Azure AD levert een algemene language infrastructure-bibliotheek met de naam [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Systeemintegrators en ontwikkelaars kunnen gebruiken van deze bibliotheek toocreate en een SCIM gebaseerde webservice-eindpunt kan verbinding maken met Azure AD tooany toepassing identiteit store implementeren.
2. Toewijzingen worden geïmplementeerd in Hallo web service toomap Hallo gestandaardiseerde gebruiker schema toohello gebruikersschema en vereist voor de toepassing hello-protocol.
3. Hallo eindpunt-URL is geregistreerd in Azure AD als onderdeel van een aangepaste toepassing in Hallo-toepassingsgalerie.
4. Gebruikers en groepen zijn toegewezen toothis toepassing in Azure AD. Bij toewijzing, worden ze in een wachtrij toobe gesynchroniseerd toohello-doeltoepassing geplaatst. synchronisatieproces Hallo Hallo wachtrij verwerking wordt uitgevoerd om de 20 minuten.

### <a name="code-samples"></a>Codevoorbeelden
toomake dit verwerken eenvoudiger, een reeks [codevoorbeelden](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) zijn opgegeven die een SCIM webservice-eindpunt maken en Demonstreer automatische inrichting. Een voorbeeld is van een provider die wordt onderhouden door een bestand met de rijen met door komma's gescheiden waarden die gebruikers en groepen vertegenwoordigt.  Hallo andere is van een provider die wordt toegepast op Hallo Amazon Web Services Identity and Access Management-service.  

**Vereisten**

* Visual Studio 2013 of hoger
* [Azure-SDK voor .NET](https://azure.microsoft.com/downloads/)
* Windows-machine die ondersteuning biedt voor Hallo ASP.NET framework 4.5 toobe gebruikt als Hallo SCIM eindpunt. Deze machine moet toegankelijk zijn vanuit de cloud Hallo
* [Een Azure-abonnement met een proefabonnement of een gelicentieerde versie van Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* Hallo Amazon AWS voorbeeld vereist bibliotheken van Hallo [AWS-Toolkit voor Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Zie voor meer informatie, Hallo Leesmij bestand wordt geleverd met Hallo-voorbeeld.

### <a name="getting-started"></a>Aan de slag
Hallo gemakkelijkste manier tooimplement een SCIM-eindpunt dat kan worden geaccepteerd inrichten van Azure AD-aanvragen is toobuild en implementeert u Hallo voorbeeldcode die Hallo ingerichte gebruikers tooa door komma's gescheiden waarden (CSV)-bestand.

**een voorbeeld SCIM eindpunt toocreate:**

1. Het downloadpakket Hallo code voorbeeld op [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Pak Hallo pakket en plaats het op uw Windows-machine op een locatie zoals C:\AzureAD-BYOA-Provisioning-Samples\.
3. In deze map starten Hallo FileProvisioningAgent oplossing in Visual Studio.
4. Selecteer **Extra > Library Package Manager > Package Manager Console**, en na-opdrachten voor Hallo FileProvisioningAgent tooresolve Hallo oplossing projectverwijzingen Hallo uitvoeren:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Hallo FileProvisioningAgent project bouwen.
6. Hallo opdrachtprompt toepassing in Windows (als Administrator) starten en gebruiken van Hallo **cd** opdracht toochange Hallo directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** map.
7. Hallo de volgende opdracht, waarbij < ip-adres > vervangt door Hallo IP-adres of domeinnaam naam van de Windows-computer Hallo uitvoeren:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. In Windows onder **Windows-instellingen > netwerk- en instellingen voor Internet**, selecteer Hallo **Windows Firewall > instellingen voor geavanceerde**, en maak een **regel voor binnenkomende verbindingen** die kan de binnenkomende toegang tooport 9000.
9. Als Windows-machine Hallo zich achter een router, Hallo router behoeften toobe geconfigureerd tooperform Network Access Translation tussen de poort 9000 die blootgestelde toohello internet en poort 9000 op Hallo Windows-computer. Dit is vereist voor Azure AD toobe kunnen tooaccess dit eindpunt in Hallo cloud.

**tooregister hello voorbeeld SCIM eindpunt in Azure AD:**

1. Aanmelden te[hello Azure-portal](https://portal.azure.com). 
2. Te bladeren ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.
3. Voer een naam voor uw toepassing en klik op **toevoegen** pictogram toocreate een app-object. Hallo application-object gemaakt is beoogde toorepresent Hallo doel app u tooand implementeren van eenmalige aanmelding voor, en niet alleen Hallo SCIM eindpunt wilt inrichten.
4. Selecteer in de resulterende welkomstscherm Hallo **inrichten** tabblad in de linkerkolom Hallo.
5. In Hallo **modus inrichting** selecteert u **automatische**.
    
  ![][2]
  *Afbeelding 4: Configureren in Azure-portal Hallo inrichting*
    
6. In Hallo **Tenant-URL** Voer Hallo internet blootgesteld URL en poort van uw eindpunt SCIM. Zou dit iets zoals http://testmachine.contoso.com:9000 of http://<ip-address>:9000/, waarbij < ip-adres > internet is Hallo blootgesteld IP adres.  
7. Als Hallo SCIM eindpunt een OAuth bearer-token van een verlener dan Azure AD vereist, wordt de kopie Hallo OAuth bearer-token in Hallo optionele vereist **geheim Token** veld. Als dit veld leeg laat, wordt Azure AD een OAuth-bearer-token van Azure AD bij elke aanvraag uitgegeven opnemen. Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.
8. Klik op Hallo **testverbinding** knop toohave Azure Active Directory poging tooconnect toohello SCIM eindpunt. Als Hallo pogingen mislukken, wordt informatie over de fout wordt weergegeven.  
9. Als Hallo pogingen tooconnect toohello toepassing slaagt, klikt u op **opslaan** toosave Hallo beheerdersreferenties.
10. In Hallo **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten. Selecteer elke één tooreview Hallo kenmerken die worden gesynchroniseerd vanuit Azure Active Directory tooyour app. kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikers en groepen in uw app voor update-bewerkingen. Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.
11. Onder **instellingen**, Hallo **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd. Alleen selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) worden gesynchroniseerd gebruikers en groepen die zijn toegewezen in Hallo **gebruikers en groepen** tabblad.
12. Zodra de configuratie voltooid is, verandert Hallo **inrichting Status** te**op**.
13. Klik op **opslaan** toostart Hallo inrichting Azure AD-service. 
14. Als alleen synchroniseren toegewezen gebruikers en groepen (aanbevolen), moet u ervoor tooselect Hallo **gebruikers en groepen** tabblad en Hallo-gebruikers en/of groepen die u wenst dat toosync toewijzen.

Nadat de initiële synchronisatie Hallo is gestart, kunt u Hallo **controlelogboeken** tabblad toomonitor voortgang, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app wordt ingericht. Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Hallo laatste stap bij het controleren van Hallo voorbeeld is tooopen hello TargetFile.csv-bestand in Hallo \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug map op uw Windows-machine. Zodra het inrichtingsproces hello wordt uitgevoerd, ziet u dit bestand Hallo details van alle toegewezen en ingericht gebruikers en groepen.

### <a name="development-libraries"></a>-Ontwikkelbibliotheken
toodevelop uw eigen webservice die toohello SCIM specificatie voldoet eerst raken met Hallo volgende bibliotheken opgegeven door Microsoft toohelp Hallo ontwikkelingsproces versnellen: 

1. Algemene Language Infrastructure (CLI) bibliotheken zijn beschikbaar voor gebruik met talen die op basis van die infrastructuur, zoals C#. Een van deze bibliotheken [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declareert een interface Microsoft.SystemForCrossDomainIdentityManagement.IProvider, weergegeven in de volgende illustratie Hallo: A ontwikkelaars met Hallo bibliotheken zou implementeren die interface met een klasse die algemeen als een provider, kan worden verwezen. Hallo-bibliotheken inschakelen Hallo developer toodeploy een webservice die toohello SCIM specificatie voldoet. Hallo-webservice kan ofwel worden gehost in Internet Information Services of een uitvoerbaar Common Language Infrastructure-assembly. Aanvraag wordt omgezet in aanroepen toohello provider methoden die zou worden geprogrammeerd door Hallo developer toooperate op sommige identity-store.
  
  ![][3]
  
2. [Express route-handlers](http://expressjs.com/guide/routing.html) beschikbaar zijn voor het parseren van node.js aanvraagobjecten die oproepen (zoals gedefinieerd door Hallo SCIM specificatie), tooa node.js-web-service vertegenwoordigt.   

### <a name="building-a-custom-scim-endpoint"></a>Het bouwen van een aangepaste SCIM-eindpunt
Hallo CLI bibliotheken gebruiken, kunnen ontwikkelaars die bibliotheken met hun services in uitvoerbaar Common Language Infrastructure assembly of in Internet Information Services hosten. Hier volgt een voorbeeld van code voor het hosten van een service binnen een uitvoerbare assembly, op het Hallo-adres http://localhost:9000: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Deze service moet een HTTP-adres en de server certificaat voor clientverificatie welke Hallo basiscertificeringsinstantie een van de volgende Hallo is hebben: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* VeriSign
* WoSign

Een certificaat voor serververificatie zijn gebonden tooa poort op een Windows-host met behulp van hulpprogramma Hallo netwerk-shell: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Hallo-waarde opgegeven voor het Hallo certhash argument is hier Hallo vingerafdruk van certificaat hello, terwijl Hallo opgegeven waarde voor Hallo appid argument een globally unique identifier is.  

in Internet Information Services toohost Hallo-service, een ontwikkelaar zou een CLA code bibliotheek-assembly met een klasse met de naam opstarten in de standaardnaamruimte Hallo van Hallo assembly bouwen.  Hier volgt een voorbeeld van deze klasse: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Afhandeling van endpoint-verificatie
Aanvragen van Azure Active Directory bevatten een OAuth 2.0-bearer-token.   Een serviceaanvraag voor de ontvangende Hallo moet verifiëren Hallo verlener als Azure Active Directory namens Hallo verwacht Azure Active Directory-tenant voor toegang tot toohello Azure Active Directory Graph-webservice.  Hallo-token Hallo verlener wordt geïdentificeerd door een claim iss, zoals 'iss': 'https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/'.  In dit voorbeeld, Hallo basisadres van de claimwaarde hello, https://sts.windows.net, Azure Active Directory wordt aangemerkt als Hallo verlener, terwijl hello relatief adres segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, wordt een unieke id van Azure Active Hallo Directory-tenant namens welke Hallo token is uitgegeven.  Als het Hallo-token is uitgegeven voor toegang tot hello Azure Active Directory Graph-webservice, klikt u vervolgens Hallo-id van die service worden 00000002-0000-0000-c000-000000000000, in Hallo-waarde van het Hallo-token aud claimen.  

Ontwikkelaars Hallo CLA bibliotheken geleverd door Microsoft voor het bouwen van een service SCIM gebruiken kunnen verifiëren aanvragen van Azure Active Directory met Hallo Microsoft.Owin.Security.ActiveDirectory pakket met de volgende stappen: 

1. Implementeren in een provider Hallo Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior eigenschap doordat het retourneren van een methode toobe wordt aangeroepen wanneer het Hallo-service wordt gestart: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Hallo code toothat methode toohave na elke aanvraag tooany Hallo-service-eindpunten die zijn geverifieerd als voorzien van een token dat is uitgegeven door Azure Active Directory namens een tenant opgegeven voor toegang tot toohello Azure AD Graph-webservice toevoegen: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Schema voor gebruikers en groepen
Azure Active Directory kunnen twee soorten resources tooSCIM webservices inrichten.  Deze typen resources zijn gebruikers en groepen.  

User-bronnen worden geïdentificeerd door Hallo schema-id, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, die is opgenomen in deze specificatie van het protocol: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  de standaardtoewijzing Hallo Hallo kenmerken van gebruikers in Azure Active Directory toohello kenmerken van urn: ietf:params:scim:schemas:extension:enterprise:2.0:User resources hieronder vindt u in de tabel 1.  

Groep resources worden geïdentificeerd door Hallo schema-id, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Tabel 2 hieronder toont Hallo standaardtoewijzing Hallo kenmerken van groepen in Azure Active Directory toohello kenmerken http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.  

### <a name="table-1-default-user-attribute-mapping"></a>Tabel 1: Standaard Gebruikerskoppeling kenmerk
| Azure Active Directory-gebruiker | urn: ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |Actieve |
| Weergavenaam |Weergavenaam |
| Fax TelephoneNumber |phoneNumbers type eq 'fax'.value |
| Voornaam |name.givenName |
| Functie |titel |
| E-mail |e-mailberichten type eq 'werk'.value |
| mailNickname |externalId |
| Manager |Manager |
| mobiele |phoneNumbers type eq 'mobiel'.value |
| object-id |id |
| Postcode |adressen type eq 'werk'.postalCode |
| proxy-adressen |e-mailberichten [Geef eq 'andere']. Waarde |
| fysieke-levering-OfficeName |adressen [Geef eq 'andere']. Indeling |
| StreetAddress |adressen type eq 'werk'.streetAddress |
| Achternaam |name.familyName |
| Telefoonnummer |phoneNumbers type eq 'werk'.value |
| primaire gebruiker-naam |Gebruikersnaam |

### <a name="table-2-default-group-attribute-mapping"></a>Tabel 2: Standaard kenmerk apparaatgroeptoewijzing
| Azure Active Directory-groep | http://schemas.Microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| Weergavenaam |externalId |
| E-mail |e-mailberichten type eq 'werk'.value |
| mailNickname |Weergavenaam |
| Leden |Leden |
| object-id |id |
| proxyAddresses |e-mailberichten [Geef eq 'andere']. Waarde |

## <a name="user-provisioning-and-de-provisioning"></a>Gebruikers inrichten en de inrichting
Hallo volgende afbeelding toont Hallo-berichten dat tooa SCIM service toomanage Hallo levenscyclus van een gebruiker in een andere identiteit store wordt verzonden naar Azure Active Directory. Hallo diagram ziet u ook hoe een SCIM service geïmplementeerd met behulp van de CLI-bibliotheken Hallo geleverd door Microsoft voor het bouwen dat dergelijke services deze aanvragen vertalen naar aanroepen toohello methoden van een provider.  

![][4]
*Afbeelding 5: Gebruikers inrichten en de inrichting reeks*

1. Azure Active Directory-query's Hallo-service voor een gebruiker met een externalId-kenmerkwaarde die overeenkomt met de Hallo mailNickname kenmerkwaarde van een gebruiker in Azure AD. Hallo-query wordt uitgedrukt als een aanvraag Hypertext Transfer Protocol (HTTP) zoals dit voorbeeld waarin jyoung een voorbeeld van een mailNickname van een gebruiker in Azure Active Directory is: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello querymethode van Hallo serviceprovider.  Hier volgt Hallo handtekening van deze methode: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Hallo-definitie van Hallo Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface Ga als volgt: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  In Hallo voorbeeld van een query voor een gebruiker met een opgegeven waarde voor Hallo externalId kenmerk te volgen, zijn waarden van Hallo argumenten doorgegeven toohello Query-methode: 
  * parameters. AlternateFilters.Count: 1
  * parameters. AlternateFilters.ElementAt(0). AttributePath: 'externalId'
  * parameters. AlternateFilters.ElementAt(0). Vergelijkingsoperator: ComparisonOperator.Equals
  * parameters. AlternateFilter.ElementAt(0). ComparisonValue: 'jyoung'
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"] 

2. Als Hallo antwoord tooa query toohello webservice voor een gebruiker met een kenmerkwaarde externalId die overeenkomt met de Hallo mailNickname kenmerkwaarde van een gebruiker niet alle gebruikers, klikt u vervolgens Azure Active Directory-aanvragen die Hallo service bepaling van een gebruiker bijbehorende toohello één in Azure Active Directory.  Hier volgt een voorbeeld van een aanvraag: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM zou die aanvraag vertalen naar een toohello aanroep van methode Create van Hallo serviceprovider.  Hallo methode Create heeft deze handtekening: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  Hallo-waarde van Hallo resource argument is in een tooprovision aanvraag een gebruiker een exemplaar van Hallo Microsoft.SystemForCrossDomainIdentityManagement. Core2EnterpriseUser klasse is gedefinieerd in Hallo Microsoft.SystemForCrossDomainIdentityManagement.Schemas-bibliotheek.  Als Hallo aanvraag tooprovision Hallo gebruiker slaagt, klikt u vervolgens is hello implementatie van Hallo-methode verwachte tooreturn een exemplaar van Hallo Microsoft.SystemForCrossDomainIdentityManagement. Core2EnterpriseUser klasse, met het Hallo-waarde van de id-eigenschap Hallo unieke id van de toohello van Hallo nieuw ingerichte gebruiker instellen.  

3. tooupdate bekend tooexist in een archief van de identiteit van een gebruiker fronted door een SCIM, Azure Active Directory uitgevoerd door het aanvragen van huidige status van die gebruiker Hallo van Hallo-service met een aanvraag, zoals: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  In een service die is gebouwd met behulp van Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM, wordt Hallo-aanvraag omgezet in een aanroep toohello ophalen-methode van Hallo serviceprovider.  Hier volgt Hallo handtekening van Hallo ophalen methode: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  In voorbeeld van een aanvraag tooretrieve Hallo huidige status van een gebruiker Hallo zijn Hallo waarden van Hallo-eigenschappen van Hallo-object opgegeven Hallo-waarde van argument Hallo-parameters als volgt uit: 
  
  * -ID: '54D382A4-2050-4C03-94D1-E769F1D15682'
  * SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'

4. Als een verwijzingskenmerk bijgewerkt, toobe vervolgens Azure Active Directory-query's Hallo service toodetermine is al dan niet hello huidige waarde van Hallo verwijzingskenmerk in archief Hallo fronted door Hallo-service al overeenkomt met de waarde van dit kenmerk Hallo in Azure Active Directory. Voor gebruikers is de enige kenmerk Hallo welke Hallo huidige waarde op deze manier wordt opgevraagd Hallo manager kenmerk. Hier volgt een voorbeeld van een aanvraag toodetermine of Hallo manager kenmerk van een bepaalde gebruiker-object momenteel een bepaalde waarde is: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Hallo waarde van kenmerken queryparameter Hallo-id, betekent dat als een gebruikersobject bestaat die voldoet aan Hallo expressie opgegeven Hallo-waarde van parameter Hallo filter-query, is Hallo service verwachte toorespond met een urn: ietf:params:scim:schemas: Core: 2.0:User of urn: ietf:params:scim:schemas:extension:enterprise:2.0:User bron, met inbegrip van alleen Hallo waarde van kenmerk van de bron-id.  waarde van Hallo Hallo **id** kenmerk toohello aanvrager is bekend. Het is opgenomen in het Hallo-waarde van de queryparameter Hallo-filter; Hallo-doel van deze vragen is daadwerkelijk toorequest een minimale representatie van een resource die voldoen aan de filterexpressie Hallo als indicatie van of deze object bestaat.   

  Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello querymethode van Hallo serviceprovider. Hallo-waarde van Hallo eigenschappen van Hallo object dat is opgegeven als Hallo-waarde van argument Hallo-parameters zijn als volgt: 
  
  * parameters. AlternateFilters.Count: 2
  * parameters. AlternateFilters.ElementAt(x). AttributePath: 'id'
  * parameters. AlternateFilters.ElementAt(x). Vergelijkingsoperator: ComparisonOperator.Equals
  * parameters. AlternateFilter.ElementAt(x). ComparisonValue: '54D382A4-2050-4C03-94D1-E769F1D15682'
  * parameters. AlternateFilters.ElementAt(y). AttributePath: 'manager'
  * parameters. AlternateFilters.ElementAt(y). Vergelijkingsoperator: ComparisonOperator.Equals
  * parameters. AlternateFilter.ElementAt(y). ComparisonValue: '2819c223-7f76-453a-919d-413861904646'
  * parameters. RequestedAttributePaths.ElementAt(0): 'id'
  * parameters. SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'

  Hier Hallo-waarde van Hallo index x mogelijk 0 en Hallo-waarde van y voor Hallo-index is mogelijk 1, of mogelijk Hallo-waarde van x 1 en Hallo-waarde van y kan zijn ingesteld op 0, afhankelijk van het Hallo-volgorde van Hallo expressies van het Hallo-filter-queryparameter.   

5. Hier volgt een voorbeeld van een aanvraag van Azure Active Directory tooan SCIM service tooupdate een gebruiker: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  Hallo Microsoft Common Language Infrastructure bibliotheken voor het implementeren van services SCIM zou Hallo aanvraag vertalen naar een toohello aanroep van methode Update van Hallo serviceprovider. Hier volgt Hallo handtekening Hallo updatemethode: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    In voorbeeld van een aanvraag tooupdate een gebruiker Hallo heeft Hallo object opgegeven Hallo-waarde van Hallo patch argument waarden van deze eigenschappen: 
  
  * ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'
  * ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'
  * (PatchRequest als PatchRequest2). Operations.Count: 1
  * (PatchRequest als PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add
  * (PatchRequest als PatchRequest2). Operations.ElementAt(0). Path.AttributePath: 'manager'
  * (PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.Count: 1
  * (PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Verwijzing: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Waarde: 2819c223-7f76-453a-919d-413861904646

6. toode inrichten een gebruiker uit een identity-store fronted door een SCIM-service, Azure AD verzendt een aanvraag, zoals: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello Delete-methode van Hallo serviceprovider.   Deze methode heeft deze handtekening: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  Hallo-object opgegeven Hallo-waarde van Hallo resourceIdentifier argument heeft deze eigenschapswaarden in Hallo voorbeeld van een aanvraag toode-bepaling van een gebruiker: 
  
  * ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'
  * ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'

## <a name="group-provisioning-and-de-provisioning"></a>Groep inrichting en ongedaan inrichten
Hallo volgende afbeelding toont Hallo-berichten dat Azure AcD tooa SCIM service toomanage Hallo levenscyclus van een groep in een andere identiteit store verzendt.  Deze berichten verschillen van Hallo-berichten die deel uitmaakt van toousers op drie manieren: 

* Hallo-schema van een bron wordt geïdentificeerd als http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Aanvragen tooretrieve groepen bepalen dat Hallo leden-kenmerk is uitgesloten van een resource in het antwoord toohello aanvraag toobe.  
* Aanvragen toodetermine aanvragen over Hallo leden kenmerk of een verwijzingskenmerk heeft voor een bepaalde waarde zijn.  

![][5]
*Afbeelding 6: Inrichting en ongedaan inrichting sequence groeperen*

## <a name="related-articles"></a>Verwante artikelen:
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Gebruiker inrichten/Deprovisioning tooSaaS Apps automatiseren](active-directory-saas-app-provisioning.md)
* [Kenmerktoewijzingen voor gebruikers inrichten aanpassen](active-directory-saas-customizing-attribute-mappings.md)
* [Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Bereikfilters voor gebruikers inrichten](active-directory-saas-scoping-filters.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
