---
title: aaaUpgrade van Mobile Services tooAzure App Service
description: Meer informatie over hoe tooeasily upgrade voor uw Mobile Services-toepassing tooan App Service-mobiele App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Upgrade van uw bestaande .NET Azure Mobile Service-tooApp Service
App Service Mobile is een nieuwe manier toobuild mobiele toepassingen met Microsoft Azure. toolearn meer, Zie [wat zijn Mobile Apps?].

Dit onderwerp wordt beschreven hoe een bestaande toepassing van .NET-back-end van Azure Mobile Services tooa tooupgrade nieuwe App Service Mobile Apps. Terwijl u deze upgrade uitvoert, kunt uw bestaande Mobile Services-toepassing toooperate blijven.   Als u een Node.js-toepassing voor back-end tooupgrade nodig hebt, raadpleegt u te[upgraden van uw Node.js Mobile Services](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Wanneer een mobiele back-end bijgewerkte tooAzure App Service is, heeft toegang tot tooall functies van de App en worden in rekening gebracht volgens te[App Service-prijzen], niet Mobile Services-prijzen.

## <a name="migrate-vs-upgrade"></a>Migreren upgraden
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Het is raadzaam dat u [uitvoeren van een migratie](app-service-mobile-migrating-from-mobile-services.md) voordat u doorgaat door middel van een upgrade. Op deze manier kunt u beide versies van uw toepassing plaatsen op Hallo van dezelfde App Service-Plan en er zijn geen extra kosten in rekening gebracht.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Verbeteringen in Mobile Apps .NET server SDK
Upgraden van nieuwe toohello [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) Hallo volgende voordelen biedt:

* Meer flexibiliteit in NuGet-afhankelijkheden. Hallo hostomgeving niet langer biedt een eigen versies van NuGet-pakketten, zodat u alternatieve compatibel versies kunt gebruiken. Als er nieuwe essentiële bugfixes of beveiliging updates toohello Mobile Server SDK of afhankelijkheden zijn, moet u handmatig een uw service bijwerken.
* Meer flexibiliteit bij het Hallo mobiele SDK. Expliciet kunt u bepalen welke functies en routes zijn ingesteld, zoals verificatie, tabel-API's, en Hallo push registratie eindpunt. toolearn meer, Zie [hoe toouse server .NET SDK voor Azure Mobile Apps Hallo](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Ondersteuning voor andere typen van ASP.NET-project en routes. Als uw mobiele back endproject kunt u nu MVC en Web-API-domeincontrollers in hetzelfde project Hallo hosten.
* Ondersteuning voor nieuwe App Service verificatiefuncties, waarmee u toouse een algemene authentication-configuratie op uw web- en mobiele apps.

## <a name="overview"></a>Upgrade basisoverzicht
In veel gevallen is upgraden net zo eenvoudig als overschakelen toohello nieuwe Mobile Apps server SDK en uw code naar een nieuw exemplaar van de mobiele App opnieuw te publiceren. Er zijn echter enkele scenario's waarvoor u enkele aanvullende configuratiestappen, zoals geavanceerde verificatie-scenario's en werken met geplande taken. Elk van deze wordt beschreven in hello later secties.

> [!TIP]
> Het wordt aanbevolen dat u lees- en Hallo rest van dit onderwerp volledig begrijpen voordat u een upgrade. Noteer van alle onderdelen gebruik die hieronder worden genoemd.
>
>

Hallo Mobile Services-client-SDK's zijn **niet** compatibel is met de Hallo nieuwe Mobile Apps server SDK. In de volgorde tooprovide continuïteit van de service voor uw app, moet u wijzigingen tooa site momenteel bedient gepubliceerde clients niet publiceren. In plaats daarvan moet u een nieuwe mobiele app die als een duplicaat fungeert maken. U kunt deze toepassing plaatsen op Hallo dezelfde App Service tooavoid steeds extra financiële kosten plannen.

U moet dan twee versies van de toepassing hello: één welke blijft dezelfde Hallo en gepubliceerde apps in Hallo wilde en Hallo fungeert andere die u kunt vervolgens een upgrade en een doel met een nieuwe client-release. U kunt verplaatsen en testen van uw code in uw tempo, maar moet u ervoor zorgen dat alle oplossingen voor problemen u toegepaste tooboth krijgen. Als u denkt dat een gewenste aantal client-apps in Hallo wilde toohello meest recente versie hebt bijgewerkt, kunt u de oorspronkelijke gemigreerde Apps Hallo verwijderen als u wenst.

Hallo volledige overzicht voor het upgradeproces Hallo is als volgt:

1. Een nieuwe mobiele App maken
2. Update Hallo project toouse Hallo nieuwe Server SDK 's
3. Een nieuwe versie van de clienttoepassing
4. (Optioneel) Verwijderen van uw oorspronkelijke gemigreerde exemplaar

## <a name="mobile-app-version"></a>Een tweede toepassingsexemplaar maken
Hallo is eerste stap bij het bijwerken van toocreate Hallo mobiele App resource die als voor de nieuwe versie Hallo van uw toepassing host fungeert. Als u al een bestaande mobiele service hebt gemigreerd, wilt u toocreate deze versie op Hallo hetzelfde hosting plan. Open Hallo [Azure-portal] en navigeer tooyour toepassing gemigreerd. Noteer Hallo App Service-Plan wordt uitgevoerd.

Maak vervolgens de tweede toepassingsexemplaar Hallo door de volgende Hallo [.NET backend maken instructies](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Vraag tooselect kiest u App Service-abonnement of 'hosting plan' Hallo wanneer plan van uw gemigreerde toepassing.

U zult waarschijnlijk toouse Hallo dezelfde database en Notification Hub als u in Mobile Services heeft. U kunt deze waarden kopiëren door het openen van [Azure-portal] en toohello oorspronkelijke toepassing navigeren, klik op **instellingen** > **toepassingsinstellingen**. Onder **verbindingsreeksen**, kopie `MS_NotificationHubConnectionString` en `MS_TableConnectionString`. Navigeer tooyour nieuwe upgraden van site en plak deze in een bestaande waarden wordt overschreven. Herhaal dit proces voor andere toepassingsinstellingen de behoeften van uw app. Als een gemigreerde service wordt niet gebruikt, kunt u verbindingsreeksen en app-instellingen lezen van Hallo **configureren** tabblad Hallo Mobile Services-sectie van Hallo [klassieke Azure-portal].

Maak een kopie van de ASP.NET-project Hallo voor uw toepassing en de nieuwe site tooyour publiceren. Met een exemplaar van de clienttoepassing bijgewerkt met de nieuwe URL hello, controleren of alles werkt zoals verwacht.

## <a name="updating-hello-server-project"></a>Hallo serverproject bijwerken
Mobiele Apps biedt een nieuwe [Mobile App Server SDK] waarmee u veel Hallo dezelfde functionaliteit als Hallo Mobile Services runtime. U moet eerst alle verwijzingen toohello Mobile Services pakketten verwijderen. Zoek in Hallo NuGet-Pakketbeheer voor `WindowsAzure.MobileServices.Backend`. De meeste apps ziet verschillende pakketten hier, met inbegrip van `WindowsAzure.MobileServices.Backend.Tables` en `WindowsAzure.MobileServices.Backend.Entity`. In dat geval moet beginnen met de laagste pakket Hallo in afhankelijkheidsstructuur hello, zoals `Entity`, en deze te verwijderen. Wanneer u wordt gevraagd, verwijder alle afhankelijke pakketten niet. Herhaal dit proces totdat u hebt verwijderd `WindowsAzure.MobileServices.Backend` zelf.

Op dit moment hebt u een project dat verwijst niet meer naar Mobile Services SDK's.

Vervolgens voegt u verwijzingen Hallo Mobile Apps SDK. Voor deze upgrade de meeste ontwikkelaars wordt toodownload en installeert u de Hallo `Microsoft.Azure.Mobile.Server.Quickstart` inpakken, zoals dit in de hele vereist set Hallo haalt.

Er zijn een aantal compilatiefouten ten gevolge van verschillen tussen Hallo SDK's, maar deze eenvoudige tooaddress zijn en worden behandeld in de rest van deze sectie Hallo.

### <a name="base-configuration"></a>Basisconfiguratie
Klik, in WebApiConfig.cs, kunt u vervangen:

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

met

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Als u toolearn meer informatie over Hallo nieuwe .NET server SDK en hoe tooadd of verwijderen van uw app-functies wenst, Zie Hallo [hoe toouse server .NET SDK Hallo] onderwerp.
>
>

Als uw app maakt gebruik van verificatiefuncties hello, moet u ook een OWIN-middleware tooregister. In dit geval moet u Hallo hierboven configuratiecode verplaatsen naar een nieuwe OWIN-Opstartklasse.

1. Hallo NuGet-pakket toevoegen `Microsoft.Owin.Host.SystemWeb` als deze niet in uw project opgenomen wordt.
2. In Visual Studio, klik met de rechtermuisknop op uw project en selecteer **toevoegen** -> **Nieuw Item**. Selecteer **Web** -> **algemene** -> **OWIN-Opstartklasse**.
3. Hallo bovenstaande code verplaatsen voor MobileAppConfiguration van `WebApiConfig.Register()` toohello `Configuration()` methode van uw nieuwe starten van de klasse.

Zorg ervoor dat Hallo `Configuration()` methode eindigt op:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Er zijn verwante tooauthentication aanvullende wijzigingen die in Hallo volledige verificatie hieronder worden besproken.

### <a name="working-with-data"></a>Werken met gegevens
In Mobile Services, de naam van de mobiele app Hallo behandeld als Hallo standaard schemanaam in Hallo Entity Framework-installatie.

tooensure die u hebt dezelfde Hallo schema wordt verwezen als voorheen gebruik Hallo tooset Hallo schema in Hallo DbContext voor uw toepassing te volgen:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Controleer of dat u hebt ingesteld als u hierboven Hallo MS_MobileServiceName. Als uw toepassing dit eerder hebt aangepast, kunt u de naam van een ander schema opgeven.

### <a name="system-properties"></a>Systeemeigenschappen
#### <a name="naming"></a>Naamgeving
Hello Azure Mobile Services-Server SDK Systeemeigenschappen altijd een dubbele onderstrepingsteken bevatten (`__`) voorvoegsel voor Hallo-eigenschappen:

* __createdAt
* __updatedAt
* __deleted
* __version

Hallo Mobile Services-client SDK's hebben speciale logica voor het parseren van Systeemeigenschappen in deze indeling.

Systeemeigenschappen hoeft niet langer een speciale indeling en Hallo na namen hebben in Azure Mobile Apps:

* CreatedAt
* updatedAt
* verwijderd
* Versie

Hallo Mobile Apps client SDK's Hallo nieuwe system eigenschappen namen gebruiken, dus er zijn geen wijzigingen vereist tooclient code. Als u rechtstreeks tooyour service waardoor REST roept vervolgens moet u uw query's dienovereenkomstig wijzigen.

#### <a name="local-store"></a>Lokale archief
Hallo wijzigingen toohello namen van eigenschappen betekent dat een lokale database offlinesynchronisatie voor Mobile Services is niet compatibel met Mobile Apps. Indien mogelijk moet u niet een upgrade van client-apps van Mobile Services tooMobile die Apps pas na wijzigingen in behandeling zijn toohello server verzonden. Hallo bijgewerkte app moet vervolgens gebruikt u de bestandsnaam van een nieuwe database.

Als een client-app is geüpgraded van Mobile Services tooMobile Apps wanneer er een offline wijzigingen in behandeling in Hallo bewerking wachtrij, moet de systeemdatabase Hallo bijgewerkte toouse Hallo nieuwe kolomnamen zijn. In iOS, kan dit worden bereikt met lightweight migraties toochange Hallo kolomnamen. Op Android- en Hallo .NET beheerde client, moet u aangepaste SQL-toorename Hallo kolommen voor de object-gegevenstabellen.

In iOS, moet u uw schema Core gegevens voor de volgende gegevens entiteiten toomatch Hallo wijzigen. Let op: eigenschappen Hallo `createdAt`, `updatedAt` en `version` niet langer een `ms_` voorvoegsel:

| Kenmerk | Type | Opmerking |
| --- | --- | --- |
| id |Tekenreeks is gemarkeerd als vereist |primaire sleutel in externe opslag |
| CreatedAt |Date |(optioneel) maps toocreatedAt systeemeigenschap |
| updatedAt |Date |(optioneel) maps tooupdatedAt systeemeigenschap |
| Versie |Tekenreeks |(optioneel) gebruikte toodetect conflicten, maps tooversion |

#### <a name="querying-system-properties"></a>Eigenschappen van het uitvoeren van query 's
In Azure Mobile Services, Systeemeigenschappen worden niet verzonden standaard, maar alleen wanneer ze worden aangevraagd met behulp van de queryreeks Hallo `__systemProperties`. Daarentegen in Azure Mobile Apps-systeem eigenschappen zijn **altijd ingeschakeld** omdat ze deel van Hallo server SDK-objectmodel uitmaken.

Deze wijziging hoofdzakelijk van invloed is op aangepaste implementaties van domein managers, zoals de uitbreidingen van `MappedEntityDomainManager`. In Mobile Services, als een client nooit alle Systeemeigenschappen-aanvragen is het mogelijk toouse een `MappedEntityDomainManager` die daadwerkelijk wijst niet alle eigenschappen. In Azure Mobile Apps veroorzaakt deze niet-toegewezen eigenschappen echter een fout in GET-query's.

Hallo gemakkelijkste manier tooresolve Hallo probleem is toomodify zodat ze van overnemen uw DTOs `ITableData` in plaats van `EntityData`. Vervolgens voegt u Hallo `[NotMapped]` kenmerk toohello velden die moeten worden weggelaten.

Hallo volgende definieert bijvoorbeeld `TodoItem` zonder system-eigenschappen:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Opmerking: als er fouten optreden op `NotMapped`, toevoegen van een referentie-assembly toohello `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Mobile Services opgenomen sommige ondersteuning voor CORS door Hallo ASP.NET CORS-oplossing. Deze laag wrapping is verwijderde toogive Hallo ontwikkelaars meer controle, zodat u rechtstreeks gebruikmaken van kunt [ASP.NET CORS-ondersteuning](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

Hallo hoofdgebieden van belang als u met behulp van CORS zijn die Hallo `eTag` en `Location` headers moeten worden toegestaan om Hallo client SDK's toowork goed.

### <a name="push-notifications"></a>Pushmeldingen
Voor pushmeldingen is Hallo hoofditem die wellicht ontbreekt in de Server SDK Hallo Hallo PushRegistrationHandler klasse. Registraties iets anders in mobiele Apps worden verwerkt en tagless registraties zijn standaard ingeschakeld. Het beheren van labels kan worden bewerkstelligd met behulp van aangepaste API's. Zie Hallo [registreren voor labels](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructies voor meer informatie.

### <a name="scheduled-jobs"></a>Geplande taken
Geplande taken worden niet is ingebouwd in Mobile Apps, zodat eventuele bestaande taken die u in uw .NET-back-end hebt moet toobe afzonderlijk bijgewerkt. Een mogelijkheid is een geplande toocreate [Web taak] op Hallo mobiele App code site. U kan ook een domeincontroller die uw taakcode instellen en configureren van Hallo [Azure Scheduler] toohit dat eindpunt op Hallo verwacht planning.

### <a name="miscellaneous-changes"></a>Diverse wijzigingen
Alle ApiControllers die worden gebruikt door een mobiele client moet nu Hallo hebben `[MobileAppController]` kenmerk. Dit is niet langer standaard opgenomen zodat andere ApiControllers toogo niet is beïnvloed door Hallo mobiele formatters.

Hallo `ApiServices` object is niet langer deel uit van Hallo SDK. tooaccess mobiele App-instellingen, kunt u Hallo volgende:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Logboekregistratie wordt daarnaast nu bereikt met Hallo standaard ASP.NET trace schrijven:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Overwegingen voor verificatie
Hallo-verificatieonderdelen van Mobile Services zijn nu in App Service-verificatie/autorisatie-functie Hallo verplaatst. U kunt meer informatie over dit inschakelen voor uw site door Hallo lezen [toevoegen verificatie tooyour mobiele app](app-service-mobile-ios-get-started-users.md) onderwerp.

Voor sommige providers, zoals AAD, Facebook en Google, moet u kunnen tooleverage Hallo bestaande registratie van uw toepassing kopiëren. U gewoon toonavigate toohello van de identiteitsprovider portal nodig hebt en een nieuwe toohello registratie van de omleidings-URL toevoegen. Configureer vervolgens de App Service-verificatie/autorisatie met Hallo client-ID en geheim.

### <a name="controller-action-authorization"></a>Controller actie autorisatie
Alle geopende exemplaren van Hallo `[AuthorizeLevel(AuthorizationLevel.User)]` kenmerk moet nu gewijzigde toouse standaard ASP.NET Hallo `[Authorize]` kenmerk. Bovendien zijn domeincontrollers nu Anoniem standaard, zoals in andere ASP.NET-toepassingen.
Als u een van de Hallo met andere AuthorizeLevel-opties, zoals Admin of toepassing, houd er rekening mee dat deze verwijderd zijn. U kunt in plaats daarvan AuthorizationFilters instellen voor gedeelde geheimen of een service-naar-service-aanroepen van AAD-Service-Principal tooenable veilig configureren.

### <a name="getting-additional-user-information"></a>Aanvullende informatie ophalen
Krijgt u extra gebruikersgegevens, inclusief toegangstokens via Hallo `GetAppServiceIdentityAsync()` methode:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Bovendien, als uw toepassing afhankelijkheden op gebruikers-id's, duurt zoals ze opslaan in een database, is het belangrijk toonote die Hallo gebruikers-id's tussen Mobile Services en App Service Mobile Apps zijn verschillend. U kunt echter nog steeds Hallo Mobile Services gebruikers-ID ophalen. Alle Hallo ProviderCredentials subklassen hebben een gebruikers-id-eigenschap. Zodat u verder gaat uit Hallo-voorbeeld vóór:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Als uw app eventuele afhankelijkheden op gebruikers-id's neemt, is het belangrijk dat u gebruikmaken van dezelfde registratie met een id-provider indien mogelijk Hallo. Gebruikers-id's zijn doorgaans binnen het bereik toohello toepassing registreren die is gebruikt, dus introductie van een nieuwe registratie kan problemen met de overeenkomende gebruikers tootheir gegevens worden gemaakt.

### <a name="custom-authentication"></a>Aangepaste verificatie
Als uw app van een aangepaste verificatie-oplossing gebruikmaakt, kunt u ervoor dat bijgewerkte Hallo-site heeft toegang tot toohello system toomake. Volg nieuwe instructies voor de aangepaste verificatie in Hallo Hallo [.NET SDK overzicht] toointegrate uw oplossing. Houd er rekening mee dat de Hallo aangepaste verificatieonderdelen nog steeds in preview zijn.

## <a name="updating-clients"></a>Clients bijwerken
Zodra u een operationele back-end voor mobiele apps hebt, kunt u werken op een nieuwe versie van uw clienttoepassing waarin deze worden verbruikt. Mobile Apps bevat ook een nieuwe versie van Hallo client-SDK's en vergelijkbare toohello serverupgrade hierboven, moet u alle verwijzingen toohello Mobile Services SDK's voordat tooremove Hallo Mobile Apps-versies installeren.

Een van de belangrijkste wijzigingen Hallo tussen versies Hallo is dat Hallo constructors niet langer zijn vereist voor de sleutel van een toepassing. U nu doorgeven gewoon Hallo-URL van uw mobiele App. Bijvoorbeeld: op Hallo .NET-clients, Hallo `MobileServiceClient` constructor is nu:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

U kunt lezen over het installeren van Hallo nieuwe SDK's en het gebruik van de nieuwe structuur Hallo via de onderstaande koppelingen voor Hallo:

* [iOS-versie 3.0.0 of hoger](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versie 2.0.0 of hoger](app-service-mobile-dotnet-how-to-use-client-library.md)

Als uw toepassing maakt gebruik van pushmeldingen, noteer Hallo specifieke registratie-instructies voor elk platform, zijn omdat er er enkele wijzigingen ook.

Wanneer u Hallo nieuwe clientversie gereed hebt, try it out in op basis van uw project bijgewerkte server. Na de validatie of deze werkt, kunt u een nieuwe versie van uw toepassing toocustomers vrijgeven. Zodra uw klanten hebben al een kans tooreceive deze updates, kunt u uiteindelijk Hallo Mobile Services versie van uw app verwijderen. Op dit moment hebt u volledig tooan App Service-mobiele App bijgewerkt met behulp van Hallo nieuwste Mobile Apps server SDK.

<!-- URLs. -->

[Azure-portal]: https://portal.azure.com/
[klassieke Azure-portal]: https://manage.windowsazure.com/
[wat zijn Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web taak]: ../app-service-web/websites-webjobs-resources.md
[hoe toouse server .NET SDK Hallo]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[App Service-prijzen]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET SDK overzicht]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
