---
title: aaaUpgrade van Mobile Services tooAzure App Service - Node.js
description: Meer informatie over hoe tooeasily upgrade voor uw Mobile Services-toepassing tooan App Service-mobiele App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Upgrade van uw bestaande Node.js Azure Mobile Service-tooApp Service
App Service Mobile is een nieuwe manier toobuild mobiele toepassingen met Microsoft Azure. toolearn meer, Zie [wat zijn Mobile Apps?].

Dit onderwerp wordt beschreven hoe een bestaande toepassing van de back-end voor Node.js van Azure Mobile Services tooa tooupgrade nieuwe App Service Mobile Apps. Terwijl u deze upgrade uitvoert, kunt uw bestaande Mobile Services-toepassing toooperate blijven.  Als u een Node.js-toepassing voor back-end tooupgrade nodig hebt, raadpleegt u te[upgraden van uw .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).

Wanneer een mobiele back-end bijgewerkte tooAzure App Service is, heeft toegang tot tooall functies van de App en worden in rekening gebracht volgens te[App Service-prijzen], niet Mobile Services-prijzen.

## <a name="migrate-vs-upgrade"></a>Migreren upgraden
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Het is raadzaam dat u [uitvoeren van een migratie](app-service-mobile-migrating-from-mobile-services.md) voordat u doorgaat door middel van een upgrade. Op deze manier kunt u beide versies van uw toepassing plaatsen op Hallo van dezelfde App Service-Plan en er zijn geen extra kosten in rekening gebracht.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Verbeteringen in Mobile Apps Node.js server SDK
Upgraden van nieuwe toohello [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) bevat veel verbeteringen, waaronder:

* Op basis van Hallo [Express framework](http://expressjs.com/en/index.html), Hallo nieuwe knooppunt SDK is lichte en tookeep up met nieuwe versies van het knooppunt wordt ontworpen dat ze afkomstig zijn uit. U kunt gedrag van de toepassing hello met Express-middleware aanpassen.
* Aanzienlijke prestatieverbeteringen vergeleken toohello Mobile Services SDK.
* U kunt nu een website host samen met uw mobiele back-end; Daarnaast is het eenvoudig tooadd hello Azure Mobile SDK tooany bestaande express.v4 toepassing.
* Gebouwd voor verschillende platforms en lokale ontwikkeling, Hallo Mobile Apps SDK kan worden ontwikkeld en lokaal uitvoeren op Windows, Linux en OS x-platforms. Het is nu eenvoudig toouse algemene knooppunt technieken zoals uitgevoerd [Mocha](https://mochajs.org/) eerdere toodeployment wordt getest.

## <a name="overview"></a>Upgrade basisoverzicht
tooaid bij het bijwerken van een Node.js back-end van Azure App Service heeft een pakket compatibiliteit verstrekt.  Na de upgrade hebt u een site niew die geïmplementeerd tooa nieuwe App Service-site worden kan.

Hallo Mobile Services-client-SDK's zijn **niet** compatibel is met de Hallo nieuwe Mobile Apps server SDK. In de volgorde tooprovide continuïteit van de service voor uw app, moet u wijzigingen tooa site momenteel bedient gepubliceerde clients niet publiceren. In plaats daarvan moet u een nieuwe mobiele app die als een duplicaat fungeert maken. U kunt deze toepassing plaatsen op Hallo dezelfde App Service tooavoid steeds extra financiële kosten plannen.

U moet dan twee versies van de toepassing hello: een blijft dezelfde Hallo en fungeert gepubliceerde apps in Hallo wild en de andere die u kunt vervolgens een upgrade en de doelserver met een nieuwe client release. U kunt verplaatsen en testen van uw code in uw tempo, maar moet u ervoor zorgen dat alle oplossingen voor problemen u toegepaste tooboth krijgen. Als u denkt dat een gewenste aantal client-apps in het wild toohello meest recente versie hebt bijgewerkt, kunt u de oorspronkelijke gemigreerde Apps Hallo verwijderen als u wenst. Hiervoor niet eventuele extra financieel kosten als gehost in Hallo dezelfde App Service plan als uw mobiele App.

Hallo volledige overzicht voor het upgradeproces Hallo is als volgt:

1. Download uw bestaande (gemigreerde) Azure Mobile Service.
2. Hallo project tooan mobiele Apps van Azure converteren met Hallo compatibiliteit-pakket.
3. Corrigeer eventuele verschillen (zoals de verificatie-instellingen).
4. De geconverteerde tooa voor mobiele Apps van Azure-project implementeert nieuwe App Service.
5. Een nieuwe versie van de clienttoepassing dat gebruik nieuwe mobiele App Hallo vrijgeven.
6. (Optioneel) Verwijder uw oorspronkelijke gemigreerde mobile service-app.

Verwijderen kan optreden wanneer verkeer niet wordt weergegeven op uw oorspronkelijke gemigreerde mobiele service.

## <a name="install-npm-package"></a>Hallo vereisten installeren
U moet [Node] installeren op uw lokale machine.  U moet ook Hallo compatibiliteit pakketten installeren.  Nadat het knooppunt is geïnstalleerd, kunt u de volgende opdracht uit een nieuwe cmd of PowerShell-prompt Hallo uitvoeren:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a>Verkrijgen van uw Azure Mobile Services-Scripts
* Meld u bij toohello [Azure Portal].
* Met behulp van **alle Resources** of **App Services**, zoeken naar uw Mobile Services-site.
* Binnen site hello, klikt u op **extra** -> **Kudu** -> **gaat** tooopen hello Kudu site.
* Klik op **Console voor foutopsporing** -> **PowerShell** tooopen Hallo-console voor foutopsporing.
* Navigeer te`site/wwwroot/App_Data/config` door te klikken op elke map op zijn beurt
* Klik op Hallo downloaden pictogram volgende toohello `scripts` directory.

Dit wordt Hallo-scripts in het ZIP-indeling gedownload.  Maak een nieuwe map op uw lokale machine en uitpakken Hallo `scripts.ZIP` bestand binnen Hallo-directory.  Hiermee maakt u een `scripts` directory.

## <a name="scaffold-app"></a>Scaffold hello nieuwe Azure Mobile Apps back-end
Hallo volgende opdracht uit met de Hallo scripts map Hallo-directory worden uitgevoerd:

```scaffold-mobile-app scripts out```

Hiermee maakt u een ondersteunde back-end voor Azure Mobile Apps in Hallo `out` directory.  Hoewel niet vereist, is het een goed idee toocheck hello `out` map in een bron code opslagplaats van uw keuze.

## <a name="deploy-ama-app"></a>Uw back-end van Azure Mobile Apps implementeren
Tijdens de implementatie moet u toodo Hallo volgende:

1. Een nieuwe mobiele App maken in Hallo [Azure Portal].
2. Voer Hallo `createViews.sql` script op basis van de database verbonden.
3. Koppeling Hallo database die is gekoppeld tooyour Mobile Service tooyour nieuwe App Service.
4. Koppelen van andere bronnen (zoals Notification Hubs)-toohello nieuwe App Service.
5. Hallo gegenereerde code tooyour nieuwe site implementeert.

### <a name="create-a-new-mobile-app"></a>Een nieuwe mobiele App maken
1. Aanmelden op Hallo [Azure Portal].
2. Klik op **+NIEUW** > **Web en mobiel** > **Mobile App** en geef een naam op voor de nieuwe back-end van Mobile App.
3. Voor Hallo **resourcegroep**, selecteer een bestaande resourcegroep of maak een nieuwe (Hallo met behulp van dezelfde naam als uw app).

    U kunt ofwel een ander App Service-abonnement selecteren of een nieuw maken. Voor meer informatie over het plannen van de App-Services en hoe een nieuw plan in een andere prijscategorie toocreate servicetier en op de gewenste locatie, Zie [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Voor Hallo **App Service-abonnement**, Hallo standaardabonnement (in Hallo [standaardcategorie](https://azure.microsoft.com/pricing/details/app-service/)) is geselecteerd. U kunt ook een ander abonnement selecteren of [een nieuw abonnement maken](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Hallo App Service-abonnement instellingen bepalen Hallo [locatie, functies, kosten en rekenresources](https://azure.microsoft.com/pricing/details/app-service/) die zijn gekoppeld aan uw app.

    Nadat u op Hallo plan besluit, klikt u op **maken**. Hiermee maakt u back-end van Hallo mobiele App.

### <a name="run-createviewssql"></a>CreateViews.SQL uitvoeren
Hallo gegenereerde app bevat een bestand met de naam `createViews.sql`.  Dit script moet worden uitgevoerd met de doeldatabase.  Hallo-verbindingsreeks voor de doeldatabase Hallo kan worden verkregen van de gemigreerde mobiele service uit Hallo **instellingen** blade onder **verbindingsreeksen**.  Dit sjabloon heet `MS_TableConnectionString`.

U kunt dit script in SQL Server Management Studio of Visual Studio kunt uitvoeren.

### <a name="link-hello-database-tooyour-app-service"></a>Koppeling Hallo Database tooyour App Service
Koppeling Hallo bestaande database tooyour App Service:

* In Hallo [Azure Portal], opent u uw App Service.
* Selecteer **alle instellingen** -> **gegevensverbindingen**.
* Klik op **+ toevoegen**.
* Selecteer in de vervolgkeuzelijst hello, **SQL-Database**
* Onder **SQL-Database**, selecteer uw bestaande database en klik vervolgens op **Selecteer**.
* Onder **verbindingsreeks**, Hallo gebruikersnaam en wachtwoord invoeren voor Hallo-database en klik vervolgens op **OK**.
* In Hallo **gegevensverbindingen toevoegen** blade, klik op **OK**.

Hallo-gebruikersnaam en wachtwoord vindt door bekijkt hello verbindingsreeks voor de doeldatabase Hallo in uw gemigreerde Mobile Service.

### <a name="set-up-authentication"></a>Verificatie instellen
Mobiele Apps van Azure kunt u de Azure Active Directory, Facebook, Google, Microsoft en Twitter verificatie tooconfigure binnen Hallo-service.  Aangepaste verificatie moet toobe afzonderlijk ontwikkeld.  Raadpleeg de Hallo [Authenticatieconcepten] documentatie en [verificatie Quick Start] documentatie voor meer informatie.  

## <a name="updating-clients"></a>Mobiele clients bijwerken
Zodra u een operationele back-end voor mobiele apps hebt, kunt u werken op een nieuwe versie van uw clienttoepassing waarin deze worden verbruikt. Mobile Apps bevat ook een nieuwe versie van Hallo client-SDK's en vergelijkbare toohello serverupgrade hierboven, moet u tooremove alle verwijzingen toohello Mobile Services SDK's voordat de installatie van de Mobile Apps-versies.

Een van de belangrijkste wijzigingen Hallo tussen versies Hallo is dat Hallo constructors niet langer zijn vereist voor de sleutel van een toepassing.
U nu doorgeven gewoon Hallo-URL van uw mobiele App. Bijvoorbeeld: op Hallo .NET-clients, Hallo `MobileServiceClient` constructor is nu:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

U kunt lezen over het installeren van Hallo nieuwe SDK's en het gebruik van de nieuwe structuur Hallo via de onderstaande koppelingen voor Hallo:

* [Android versie 2.2 of hoger](app-service-mobile-android-how-to-use-client-library.md)
* [iOS-versie 3.0.0 of hoger](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versie 2.0.0 of hoger](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova-versie 2.0 of hoger](app-service-mobile-cordova-how-to-use-client-library.md)

Als uw toepassing maakt gebruik van pushmeldingen, noteer Hallo specifieke registratie-instructies voor elk platform, zijn omdat er er enkele wijzigingen ook.

Wanneer u Hallo nieuwe clientversie gereed hebt, try it out in op basis van uw project bijgewerkte server. Na de validatie of deze werkt, kunt u een nieuwe versie van uw toepassing toocustomers vrijgeven. Zodra uw klanten hebben al een kans tooreceive deze updates, kunt u uiteindelijk Hallo Mobile Services versie van uw app verwijderen. Op dit moment hebt u volledig tooan App Service-mobiele App bijgewerkt met behulp van Hallo nieuwste Mobile Apps server SDK.

<!-- URLs. -->

[Azure Portal]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[wat zijn Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[App Service-prijzen]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Authenticatieconcepten]: ../app-service/app-service-authentication-overview.md
[verificatie Quick Start]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
