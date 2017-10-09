---
title: aaaHow toowork met back-endserver voor Hallo .NET SDK voor Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toowork met .NET back-endserver SDK Hallo voor Azure App Service Mobile Apps.
keywords: App service, azure app service, mobiele app, mobiele service, schaal, schaalbaar, app-implementatie, azure app-implementatie
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Dit onderwerp leest u hoe toouse Hallo .NET back-endserver SDK in de belangrijkste scenario's voor Azure App Service Mobile Apps. Hello Azure Mobile Apps SDK kunt u werken met mobiele clients van uw ASP.NET-toepassing.

> [!TIP]
> Hallo [server .NET SDK voor Azure Mobile Apps] [ 2] is open-source op GitHub. Hallo-opslagplaats bevat alle broncode inclusief Hallo hele server SDK-eenheid test suite en sommige-voorbeeldprojecten.
>
>

## <a name="reference-documentation"></a>Referentiedocumentatie
Hallo-naslagdocumentatie voor Hallo server SDK bevindt zich hier: [Azure Mobile Apps .NET Reference][1].

## <a name="create-app"></a>Procedure: een mobiele App voor .NET-back-end maken
Als u een nieuw project begint, kunt u een App Service-toepassing met behulp van beide Hallo [Azure-portal] of Visual Studio. U kunt Hallo App Service-toepassing lokaal uitvoeren of Hallo project tooyour cloud-gebaseerde App Service mobiele app publiceren.

Als u mobiele mogelijkheden tooan bestaand project toevoegen wilt, Zie Hallo [downloaden en te initialiseren Hallo SDK](#install-sdk) sectie.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Maken van een .NET-backend met hello Azure-portal
een App Service mobiele back-end toocreate, ofwel Volg Hallo [Quick Start-zelfstudie] [ 3] of als volgt te werk:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Terug in Hallo *aan de slag* blade onder **maken van een tabel-API**, kies **C#** als uw **back-endtaal**. Klik op **downloaden**, pak de gecomprimeerde project bestanden tooyour lokale computer en open Hallo oplossing in Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Maken van een .NET-backend met behulp van Visual Studio 2013 en Visual Studio 2015
Hallo installeren [Azure SDK voor .NET] [ 4] (versie 2.9.0 of hoger) toocreate een Azure Mobile Apps-project in Visual Studio. Nadat u Hallo SDK hebt geïnstalleerd, maakt u een ASP.NET-toepassing hello stappen te volgen met:

1. Open Hallo **nieuw Project** dialoogvenster (van *bestand* > **nieuw** > **Project wordt gemaakt...** ).
2. Vouw **sjablonen** > **Visual C#**, en selecteer **Web**.
3. Selecteer **ASP.NET-webtoepassing**.
4. Vul in Hallo projectnaam. Klik vervolgens op **OK**.
5. Onder *ASP.NET 4.5.2-sjabloon sjablonen*, selecteer **mobiele Apps van Azure**. Controleer **hosten in de cloud Hallo** toocreate een mobiele back-end in Hallo cloud toowhich kunt u dit project publiceren.
6. Klik op **OK**.

## <a name="install-sdk"></a>Hoe: downloaden en te initialiseren Hallo SDK
Hallo SDK is beschikbaar via [NuGet.org]. Dit pakket bevat Hallo basisfunctionaliteit vereist tooget gestart met behulp van Hallo SDK. tooinitialize Hallo SDK, moet u tooperform acties op Hallo **HttpConfiguration** object.

### <a name="install-hello-sdk"></a>Hallo SDK installeren
tooinstall hello SDK, klik met de rechtermuisknop op Hallo serverproject in Visual Studio, selecteer **NuGet-pakketten beheren**, zoekt u Hallo [Microsoft.Azure.Mobile.Server] van het pakket en klik vervolgens op  **Installeer**.

### <a name="server-project-setup"></a>Hallo serverproject initialiseren
Een .NET-back-end-serverproject is geïnitialiseerd vergelijkbare tooother ASP.NET projecten, met inbegrip van een OWIN-Opstartklasse. Zorg ervoor dat u verwijst naar de NuGet-pakket Hallo `Microsoft.Owin.Host.SystemWeb`. tooadd deze klasse in Visual Studio met de rechtermuisknop op uw server-project en selecteer **toevoegen** >
**Nieuw Item**, klikt u vervolgens **Web**  >  ** Algemene** > **OWIN-Opstartklasse**.  Een klasse wordt gegenereerd met Hallo kenmerk te volgen:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

In Hallo `Configuration()` methode van uw OWIN-Opstartklasse gebruik een **HttpConfiguration** object tooconfigure hello Azure Mobile Apps-omgeving.
Hallo volgt initialiseert Hallo serverproject met geen extra functies:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable afzonderlijke functies, moet u uitbreidingsmethoden aanroepen op Hallo **MobileAppConfiguration** object voordat u **ApplyTo**. Hallo volgende code wordt bijvoorbeeld toegevoegd Hallo standaard routeert tooall API-domeincontrollers die het Hallo-kenmerk `[MobileAppController]` tijdens de initialisatie:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

Hallo server Quick Start vanuit Azure portal aanroepen Hallo **UseDefaultConfiguration()**. Deze equivalente toohello na de installatie:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

Hallo uitbreidingsmethoden zijn:

* `AddMobileAppHomeController()`biedt Hallo standaard Azure Mobile Apps-startpagina.
* `MapApiControllers()`aangepaste API biedt voor WebAPI-controllers gedecoreerd worden met Hallo `[MobileAppController]` kenmerk.
* `AddTables()`bevat een toewijzing van Hallo `/tables` eindpunten tootable domeincontrollers.
* `AddTablesWithEntityFramework()`is een korte voorhanden voor toewijzing Hallo `/tables` eindpunten met behulp van Entity Framework op basis van domeincontrollers.
* `AddPushNotifications()`biedt een eenvoudige methode voor het registreren van apparaten voor Notification Hubs.
* `MapLegacyCrossDomainController()`biedt standaard CORS-headers voor lokale ontwikkeling.

### <a name="sdk-extensions"></a>SDK-extensies
Hallo-op basis van het NuGet-extensiepakketten te volgen bieden verschillende mobiele functies die kunnen worden gebruikt door uw toepassing. U uitbreidingen inschakelen tijdens de initialisatie met Hallo **MobileAppConfiguration** object.

* [Microsoft.Azure.Mobile.Server.Quickstart] ondersteunt Hallo basisinstellingen Mobile Apps. Toegevoegde toohello configuratie door de aanroepende Hallo **UseDefaultConfiguration** extensiemethode tijdens de initialisatie. Deze extensie bevat de volgende extensies: meldingen, verificatie, entiteit, tabellen, verschillende domeinen en thuis-pakketten. Dit pakket wordt gebruikt door Hallo Mobile Apps Quick Start op Hallo Azure-portal beschikbaar.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Hallo standaard implementeert *deze mobiele app is actief en werkend pagina* voor Hallo website hoofdmap. Toohello configuratie toevoegen door het aanroepen van de **AddMobileAppHomeController** extensiemethode.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) bevat klassen voor het werken met gegevens en sets-up Hallo data pipeline. Toohello configuratie toevoegen door de aanroepende Hallo **AddTables** extensiemethode.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) kunnen Hallo Entity Framework tooaccess gegevens in Hallo SQL-Database. Toohello configuratie toevoegen door de aanroepende Hallo **AddTablesWithEntityFramework** extensiemethode.
* [Microsoft.Azure.Mobile.Server.Authentication] schakelt verificatie en sets-up Hallo OWIN middleware toovalidate tokens gebruikt. Toohello configuratie toevoegen door de aanroepende Hallo **AddAppServiceAuthentication** en **IAppBuilder**. **UseAppServiceAuthentication** uitbreidingsmethoden.
* [Microsoft.Azure.Mobile.Server.Notifications] maakt het mogelijk pushmeldingen en definieert een push-eindpunt voor registratie. Toohello configuratie toevoegen door de aanroepende Hallo **AddPushNotifications** extensiemethode.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) maakt u een domeincontroller die gegevens toolegacy webbrowsers vanuit uw mobiele App fungeert. Toohello configuratie toevoegen door het aanroepen van de **MapLegacyCrossDomainController** extensiemethode.
* [Microsoft.Azure.Mobile.Server.Login] hello AppServiceLoginHandler.CreateToken() methode, die een statische methode die wordt gebruikt tijdens aangepaste verificatie scenario's biedt.

## <a name="publish-server-project"></a>Hoe: Hallo serverproject publiceren
Deze sectie leest u hoe toopublish uw .NET-back-end project in Visual Studio. U kunt ook uw back endproject met Git implementeren of een van de andere methoden behandeld in Hallo Hallo [Implementatiedocumentatie voor Azure App Service](../app-service-web/web-sites-deploy.md).

1. In Visual Studio opnieuw worden opgebouwd Hallo project toorestore NuGet-pakketten.
2. Klik in Solution Explorer met de rechtermuisknop op Hallo-project op **publiceren**. Hallo moet eerste keer dat u publiceert, u een publicatieprofiel toodefine. Wanneer u al een profiel dat is gedefinieerd hebt, kunt u selecteren en op **publiceren**.
3. Als u wordt gevraagd tooselect een doel publiceren, klikt u op **Microsoft Azure App Service** > **volgende**, en (indien nodig) aanmelden met uw Azure-referenties.
   Visual Studio downloadt en veilig opgeslagen uw publicatie-instellingen rechtstreeks uit Azure.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Kies uw **abonnement**, selecteer **brontype** van **weergave**, vouw **mobiele App**, en klikt u op back-end van uw mobiele App en klik vervolgens op **OK**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Controleer of Hallo profielgegevens publiceren en klik op **publiceren**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Als uw back-end voor de mobiele App is gepubliceerd, ziet u een startpagina die slagen aangeeft.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a>Procedure: een tabel controller definiëren
Een tabel Controller tooexpose een SQL-tabel toomobile clients definiëren.  Een tabel Controller configureren, moet drie stappen:

1. Maak een klasse gegevens overbrengen Object (DTO).
2. Configureer een tabelverwijzing in Hallo Mobile DbContext-klasse.
3. Maak een tabel-domeincontroller.

Een Data Transfer Object (DTO) is een gewone C#-object dat eigenschappen van overneemt `EntityData`.  Bijvoorbeeld:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Hallo DTO is gebruikte toodefine Hallo tabel binnen Hallo SQL-database.  Hallo toocreate vermelding van de database, het toevoegen van een `DbSet<>` eigenschap op Hallo van DbContext die u gebruikt.  In Hallo project standaardsjabloon voor Azure Mobile Apps hello DbContext heet `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Als u hello die Azure SDK geïnstalleerd hebt, kunt u een sjabloon tabel controller nu als volgt maken:

1. Met de rechtermuisknop op de map Hallo-Controllers en selecteer **toevoegen** > **Controller...** .
2. Selecteer Hallo **Azure Mobile Apps tabel Controller** optie en klik vervolgens op **toevoegen**.
3. In Hallo **Controller toevoegen** dialoogvenster:
   * In Hallo **Modelklasse** vervolgkeuzelijst, selecteer uw nieuwe DTO.
   * In Hallo **DbContext** vervolgkeuzelijst, selecteer Hallo Mobile Service DbContext-klasse.
   * naam van de domeincontroller Hallo is voor u gemaakt.
4. Klik op **Add**.

Hallo Quick Start-serverproject bevat een voorbeeld van een eenvoudige **TodoItemController**.

### <a name="adjust-pagesize"></a>Hoe: Hallo tabel paginering grootte aanpassen
Azure Mobile Apps retourneert standaard 50 records per aanvraag.  Paginering zorgt ervoor dat clientcomputers Hallo komt niet bezighouden hun gebruikersinterface-thread noch Hallo server te lang een goede gebruikerservaring gezorgd. toochange hello tabel paginering grootte toename Hallo serverzijde 'toegestane grootte van de query' en hello clientzijde pagina grootte Hallo serverzijde 'toegestane grootte van de query' is aangepast met Hallo `EnableQuery` kenmerk:

    [EnableQuery(PageSize = 500)]

Zorg ervoor Hallo PageSize Hallo dezelfde of een groter is dan Hallo door Hallo-client wordt aangevraagd.  Raadpleeg toohello specifieke client procedure documentatie voor meer informatie over het wijzigen van het paginaformaat Hallo-client.

## <a name="how-to-define-a-custom-api-controller"></a>Procedure: een aangepaste API-controller definiëren
Hallo aangepaste API-controller biedt Hallo meest eenvoudige functionaliteit tooyour backend voor mobiele Apps bij het blootstellen van een eindpunt. U kunt een API-controller van het mobiele-specifieke met kenmerk [MobileAppController] Hallo registreren. Hallo `MobileAppController` kenmerk registreert Hallo route, stelt Hallo Mobile Apps JSON serialisatiefunctie en Hiermee schakelt u [controle van de client versie](app-service-mobile-client-and-server-versioning.md).

1. Klik in Visual Studio met de rechtermuisknop op Hallo domeincontrollers map **toevoegen** > **Controller**, selecteer **Web API 2-Controller&mdash;leeg** en Klik op **toevoegen**.
2. Geef een **controllernaam**, zoals `CustomController`, en klik op **toevoegen**.
3. Voeg toe Hallo volgende Hallo nieuwe controller klassebestand met de instructie:

        using Microsoft.Azure.Mobile.Server.Config;
4. Toepassing hello **[MobileAppController]** toohello API-controller klassendefinitie, zoals in het volgende voorbeeld Hallo kenmerk:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. Voeg in App_Start/Startup.MobileApp.cs-bestand, een aanroep van toohello **MapApiControllers** uitbreidingsmethode, zoals in het volgende voorbeeld Hallo:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

U kunt ook Hallo `UseDefaultConfiguration()` extensiemethode in plaats van `MapApiControllers()`. Elke domeincontroller die geen **MobileAppControllerAttribute** toegepast nog steeds toegankelijk zijn voor clients, maar deze kan niet worden correct gebruikt door clients met behulp van een client voor mobiele App SDK.

## <a name="how-to-work-with-authentication"></a>Procedure: werken met verificatie
Mobiele Apps van Azure maakt gebruik van App Service-verificatie / autorisatie toosecure uw mobiele back-end.  Deze sectie leest u hoe tooperform Hallo na verificatie-gerelateerde taken in uw project met .NET back-end-server:

* [Procedure: verificatie tooa serverproject toevoegen](#add-auth)
* [Procedure: aangepaste verificatie voor uw toepassing gebruiken](#custom-auth)
* [Hoe: ophalen geverifieerde gebruikersgegevens](#user-info)
* [Hoe: beperken van toegang tot gegevens voor gemachtigde gebruikers](#authorize)

### <a name="add-auth"></a>Procedure: verificatie tooa serverproject toevoegen
U kunt verificatie tooyour serverproject toevoegen door uit te breiden Hallo **MobileAppConfiguration** object en OWIN middleware configureren. Wanneer u Hallo installeert [Microsoft.Azure.Mobile.Server.Quickstart] pakket en aanroep Hallo **UseDefaultConfiguration** uitbreidingsmethode, kunt u toostep 3 overslaan.

1. In Visual Studio, installeert u Hallo [Microsoft.Azure.Mobile.Server.Authentication] pakket.
2. Voeg volgende regel code aan begin Hallo HALLO hallo in Hallo Startup.cs project-bestand **configuratie** methode:

        app.UseAppServiceAuthentication(config);

    Dit onderdeel OWIN-middleware valideert tokens die zijn uitgegeven door App Service-gateway Hallo die zijn gekoppeld.
3. Hallo toevoegen `[Authorize]` kenmerk tooany controller of methode die verificatie vereist.

toolearn over het tooauthenticate clients tooyour back-end van Mobile Apps Zie [toevoegen verificatie tooyour app](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Procedure: aangepaste verificatie voor uw toepassing gebruiken
Als u niet dat toouse een van de App Service-verificatie/autorisatie-providers hello wenst, kunt u uw eigen systeem aanmelding implementeren. Hallo installeren [Microsoft.Azure.Mobile.Server.Login] tooassist met verificatie token genereren van het pakket.  Geef uw eigen code voor het valideren van gebruikersreferenties. U kunt bijvoorbeeld controleren tegen gezouten en hash-wachtwoorden in een database. Hallo in Hallo onderstaand voorbeeld `isValidAssertion()` methode (elders gedefinieerd) is verantwoordelijk voor deze controles.

Hallo aangepaste verificatie wordt blootgelegd door een ApiController maken en blootstellen `register` en `login` acties. Hallo-client moet een aangepaste UI toocollect Hallo-informatie van Hallo-gebruiker gebruiken.  Hallo-informatie wordt verzonden toohello API met een standaard HTTP POST-aanroep. Zodra het Hallo-server valideert Hallo verklaring, een token is uitgegeven met Hallo `AppServiceLoginHandler.CreateToken()` methode.  Hallo ApiController **beter niet** hello gebruiken `[MobileAppController]` kenmerk.

Een voorbeeld `login` actie:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

In de Hallo voorgaande voorbeeld, zijn LoginResult en LoginResultUser serialiseerbaar objecten blootstellen vereiste eigenschappen. Hallo client verwacht aanmelding antwoorden toobe geretourneerd als JSON-objecten van het formulier Hallo:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Hallo `AppServiceLoginHandler.CreateToken()` methode bevat een *doelgroep* en een *verlener* parameter. Beide parameters zijn toohello-URL van de hoofdmap van uw toepassing met behulp van HTTPS-schema Hallo ingesteld. U moet op dezelfde manier instellen *secretKey* toobe Hallo-waarde van uw toepassing de handtekeningsleutel. Hallo ondertekening sleutel in een client kan worden gebruikt toomint sleutels en gebruikers te imiteren niet distribueren. Kunt u de handtekeningsleutel terwijl die in App Service wordt gehost door te verwijzen naar Hallo Hallo *WEBSITE\_AUTH\_ondertekening\_sleutel* omgevingsvariabele. Indien nodig in de context van een lokale foutopsporing, volgt u de instructies Hallo in Hallo [lokale foutopsporing met verificatie](#local-debug) sectie tooretrieve Hallo sleutel en op te slaan als een toepassingsinstelling.

Hallo uitgegeven token mogelijk ook andere claims en een vervaldatum.  Minimaal Hallo uitgegeven token vergezeld gaan van een onderwerp (**sub**) claim.

U kunt standaard client Hallo ondersteunen `loginAsync()` methode door Hallo verificatie route overbelasting.  Als de client Hallo aanroept `client.loginAsync('custom');` toolog in uw route moet `/.auth/login/custom`.  U kunt instellen Hallo route voor het gebruik van Hallo aangepaste verificatie controller `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Met behulp van Hallo `loginAsync()` aanpak zorgt ervoor dat Hallo-verificatietoken is gekoppeld tooevery volgende aanroep toohello service.
>
>

### <a name="user-info"></a>Hoe: ophalen geverifieerde gebruikersgegevens
Wanneer een gebruiker is geverifieerd door App Service, kunt u toegang tot Hallo toegewezen gebruikers-ID en andere informatie die in uw .NET-back-end-code. Hallo gebruikersgegevens kan worden gebruikt voor het nemen van autorisatiebeslissingen in Hallo back-end. Hallo haalt volgende code Hallo gebruikers-ID die is gekoppeld aan een aanvraag:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hallo SID is afgeleid van Hallo provider-specifieke gebruikers-ID en statisch voor een bepaalde gebruiker en de aanmeldingsprovider.  Hallo SID is null voor ongeldige verificatietokens.

App Service kunt u bepaalde claims aanvragen bij uw aanmeldingsprovider. Elke identiteitsprovider krijgt u meer informatie, met behulp van de identiteitsprovider SDK.  U kunt bijvoorbeeld Hallo Facebook Graph API gebruiken voor vrienden informatie.  Hallo provider blade in hello Azure-portal kunt u claims die worden aangevraagd. Sommige claims nodig aanvullende configuratie met de id-provider Hallo.

Hallo volgende code aanroepen Hallo **GetAppServiceIdentityAsync** extensie methode tooget Hallo aanmeldingsreferenties, waaronder Hallo toegangsaanvragen token benodigde toomake tegen Hallo Facebook Graph API:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Toevoegen van een instructie voor `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extensiemethode.

### <a name="authorize"></a>Hoe: beperken van toegang tot gegevens voor gemachtigde gebruikers
In de vorige sectie hello bleek we hoe tooretrieve Hallo gebruikers-ID van een geverifieerde gebruiker. U kunt beperken toodata toegang en andere bronnen op basis van deze waarde. Een kolom userId tootables toe te voegen en het filteren van Hallo queryresultaten door Hallo gebruikers-ID is bijvoorbeeld een eenvoudige manier toolimit gegevens alleen tooauthorized gebruikers geretourneerd. Hallo retourneert volgende code rijen met gegevens alleen als Hallo SID overeenkomt met de waarde in Hallo UserId kolom in de takentabel Hallo:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Hallo `Query()` methode retourneert een `IQueryable` die kan worden bewerkt door LINQ toohandle filteren.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Hoe: push notifications tooa serverproject toevoegen
Push notifications tooyour serverproject toevoegen door uit te breiden Hallo **MobileAppConfiguration** object en het maken van een client Notification Hubs.

1. In Visual Studio met de rechtermuisknop op het serverproject Hallo en klikt u op **NuGet-pakketten beheren**, zoeken naar `Microsoft.Azure.Mobile.Server.Notifications`, klikt u vervolgens op **installeren**.
2. Herhaal deze stap tooinstall hello `Microsoft.Azure.NotificationHubs` pakket, waaronder Hallo Notification Hubs-clientbibliotheek.
3. In App_Start/Startup.MobileApp.cs, en voeg een aanroep van toohello **AddPushNotifications()** extensiemethode tijdens de initialisatie:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Na de code die wordt gemaakt van een client Notification Hubs Hallo toevoegen:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

U kunt nu Hallo Notification Hubs toosend push notifications tooregistered clientapparaten gebruiken. Zie voor meer informatie [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md). Zie toolearn meer informatie over Notification Hubs [overzicht van Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Hoe: Enable gericht push met Tags
Notification Hubs kunt u toospecific registraties van gerichte meldingen verzenden met behulp van codes. Verschillende labels worden automatisch gemaakt:

* Hallo installatie-ID identificeert een specifiek apparaat.
* Hallo gebruikers-Id op basis van Hallo geverifieerde SID identificeert een specifieke gebruiker.

installatie-ID toegankelijk zijn vanuit Hallo Hallo **omwille van** -eigenschap op Hallo **MobileServiceClient**.  Hallo volgende voorbeeld ziet u hoe u een installatie-ID tooadd een tag tooa specifieke installatie in Notification Hubs:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Labels verstrekt door Hallo client tijdens de registratie voor pushberichten worden genegeerd door Hallo back-end bij het maken van Hallo-installatie. een client tooadd tooenable tags toohello installatie, moet u een aangepaste API gebruiken waarmee labels Hallo vóór het patroon wordt toegevoegd.

Zie [Client toegevoegd push notification-tags] [ 5] in Hallo App Service Mobile Apps voltooide Quick Start-voorbeeld voor een voorbeeld.

## <a name="push-user"></a>Hoe: verzenden push notifications tooan geverifieerde gebruiker
Wanneer een geverifieerde gebruiker geregistreerd voor pushmeldingen, wordt een gebruikers-ID-tag toohello registratie automatisch toegevoegd. Met deze code, kunt u push notifications tooall apparaat hebt geregistreerd met deze persoon verzenden. Hallo volgende code wordt Hallo SID van de gebruiker die de aanvraag en verzendt een sjabloon tooevery apparaatregistratie voor pushberichten voor deze persoon:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Wanneer u registreert voor pushmeldingen vanuit een geverifieerde client, moet u ervoor zorgen dat de verificatie is voltooid voordat u de registratie. Zie voor meer informatie [Push toousers] [ 6] in Hallo App Service Mobile Apps voltooide Quick Start-voorbeeld voor .NET-back-end.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Procedure: fouten opsporen en oplossen van Hallo SDK voor .NET-Server
Azure App Service biedt verschillende opsporen en oplossen van technieken voor ASP.NET-toepassingen:

* [Bewaking van een Azure App Service](../app-service-web/web-sites-monitor.md)
* [Diagnostische logboekregistratie in Azure App Service inschakelen](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Een Azure App Service in Visual Studio oplossen](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Logboekregistratie
U kunt tooApp Service diagnostische logboeken schrijven met behulp van Hallo standaard ASP.NET trace schrijven. Voordat u toohello logboeken schrijven kan, moet u diagnostische gegevens inschakelen in uw back-end voor de mobiele App.

tooenable diagnostische gegevens en schrijven toohello Logboeken:

1. Volg de stappen Hallo in [hoe diagnostische gegevens tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Voeg de volgende Hallo in uw codebestand met de instructie:

        using System.Web.Http.Tracing;
3. Maakt een tracering writer toowrite Hallo .NET backend toohello diagnostische logboeken, als volgt:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Publiceren van uw serverproject en toegang tot het Hallo mobiele App back-end tooexecute Hallo codepad met de Hallo logboekregistratie.
5. Downloaden en te evalueren Hallo Logboeken, zoals beschreven in [hoe: Logboeken downloaden](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Lokale foutopsporing met verificatie
U kunt uw toepassing uitvoeren lokaal tootest gewijzigd voordat u ze toohello cloud publiceert. Druk op voor de meeste Azure Mobile Apps back-ends, *F5* tijdens het in Visual Studio. Er zijn echter enkele aanvullende overwegingen bij het gebruik van verificatie.

Er moet een cloud-gebaseerde mobiele app met App Service-verificatie/autorisatie geconfigureerd en uw client hello cloudeindpunt opgegeven als Hallo alternatieve aanmeldings-host moet hebben. Zie Hallo-documentatie voor uw clientplatform voor Hallo specifieke stappen vereist.

Zorg ervoor dat uw mobiele back-end [Microsoft.Azure.Mobile.Server.Authentication] geïnstalleerd. Voeg in uw toepassing OWIN-Opstartklasse volgende hello, na `MobileAppConfiguration` is toegepaste tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

In de Hallo voorgaande voorbeeld, moet u configureren Hallo *authAudience* en *authIssuer* toepassingsinstellingen binnen uw Web.config bestand tooeach worden de URL van de hoofdmap van uw toepassing hello HTTPS gebruiken schema. U moet op dezelfde manier instellen *authSigningKey* toobe Hallo-waarde van uw toepassing de handtekeningsleutel.
tooobtain hello ondertekeningssleutel:

1. Navigeer tooyour app binnen Hallo [Azure-portal]
2. Klik op **extra**, **Kudu**, **gaat**.
3. Klik op Hallo Kudu Management site **omgeving**.
4. Hallo-waarde voor *WEBSITE\_AUTH\_ondertekening\_sleutel*.

Gebruik Hallo ondertekeningssleutel voor Hallo *authSigningKey* parameter in de configuratie van uw lokale toepassingen.  Uw mobiele back-end is nu ingericht toovalidate tokens bij lokale uitvoering waarin clientcomputers Hallo Hallo token van een cloud-gebaseerde Hallo-eindpunt verkrijgt.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure-portal]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
