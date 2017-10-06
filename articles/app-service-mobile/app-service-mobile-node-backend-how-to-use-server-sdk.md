---
title: aaaHow toowork met back-endserver voor Hallo Node.js SDK voor Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toowork met back-endserver voor Node.js SDK Hallo voor Azure App Service Mobile Apps.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Hoe toouse hello Azure Mobile Apps Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Dit artikel vindt u gedetailleerde informatie over en voorbeelden ziet u hoe toowork met een back-end voor Node.js in Azure App Service Mobile Apps.

## <a name="Introduction"></a>Inleiding
Azure App Service Mobile Apps biedt Hallo mogelijkheid tooadd mobile-geoptimaliseerde gegevenstoegang Web API tooa webtoepassing.  Hello Azure App Service Mobile Apps SDK is beschikbaar voor ASP.NET- en Node.js-webtoepassingen.  Hallo SDK biedt Hallo volgende bewerkingen:

* Tabelbewerkingen (lezen, Insert, Update, Delete) voor toegang tot gegevens
* Aangepaste API-bewerkingen

Beide bewerkingen kunnen worden gebruikt voor verificatie binnen alle id-providers toegestaan door Azure App Service, met inbegrip van sociale id-providers zoals Facebook, Twitter, Google en Microsoft, evenals Azure Active Directory voor de identiteit van de onderneming.

U vindt voorbeelden voor elk gebruiksvoorbeeld in Hallo [directory voorbeelden op GitHub].

## <a name="supported-platforms"></a>Ondersteunde Platforms
Hello Azure Mobile Apps knooppunt SDK biedt ondersteuning voor Hallo die huidige TNS bij de release van knooppunt en later.  Op moment van schrijven is het meest recente TNS versie Hallo knooppunt v4.5.0.  Andere versies van knooppunt werkt, maar worden niet ondersteund.

Hello Azure Mobile Apps knooppunt SDK ondersteunt twee databasestuurprogramma - hello knooppunt mssql-stuurprogramma ondersteunt SQL Azure en lokale exemplaren van SQL Server.  Hallo sqlite3 stuurprogramma ondersteunt SQLite-databases in één exemplaar.

### <a name="howto-cmdline-basicapp"></a>Procedure: een eenvoudige Node.js back-end met Hallo opdrachtregel maken
Elke back-end van Azure App Service Mobile App Node.js wordt gestart als een toepassing ExpressJS.  ExpressJS is Hallo meest populaire web service framework beschikbaar voor Node.js.  U kunt een eenvoudige maken [Express] toepassing als volgt:

1. Maak een map voor uw project in een opdracht of een PowerShell-venster.

        mkdir basicapp
2. Pakketstructuur van npm init tooinitialize Hallo worden uitgevoerd.

        cd basicapp
        npm init

    Hallo npm init-opdracht wordt u gevraagd een reeks vragen tooinitialize Hallo project.  Zie Hallo voorbeeld van uitvoer:

    ![Hallo npm init-uitvoer][0]
3. Hallo snelle en apps van azure mobile bibliotheken van de npm-opslagplaats Hallo installeren.

        npm install --save express azure-mobile-apps
4. Maak een app.js tooimplement Hallo basic mobiele-bestandsserver.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Deze toepassing maakt een WebAPI mobile geoptimaliseerd met één eindpunt (`/tables/TodoItem`) waarmee niet-geverifieerde toegang tooan onderliggende SQL-gegevensopslag met behulp van een dynamische schema.  Is geschikt voor een snel starten van de client-bibliotheek te volgen:

* [Android Client Quick Start]
* [Apache Cordova-Client Quick Start]
* [iOS-Client Quick Start]
* [Windows Store-Client Quick Start]
* [Quick Start voor Xamarin.iOS-Client]
* [Snelstartgids voor Xamarin.Android-Client]
* [Quick Start Xamarin.Forms-Client]

Hallo code vindt u voor deze eenvoudige toepassing in Hallo [basicapp voorbeeld op GitHub].

### <a name="howto-vs2015-basicapp"></a>Procedure: een back-end knooppunt maken met Visual Studio 2015
Visual Studio 2015 is een uitbreiding toodevelop Node.js-toepassingen binnen Hallo IDE vereist.  toostart, installatie Hallo [1.1 van Node.js-hulpprogramma's voor Visual Studio].  Zodra Hallo Node.js-Tools voor Visual Studio zijn geïnstalleerd, moet u een snelle 4.x-toepassing maken:

1. Open Hallo **nieuw Project** dialoogvenster (van **bestand** > **nieuw** > **Project wordt gemaakt...** ).
2. Vouw **sjablonen** > **JavaScript** > **Node.js**.
3. Selecteer Hallo **Azure Node.js Express 4 basistoepassing**.
4. Vul in Hallo projectnaam.  Klik op *OK*.

    ![Nieuw Project voor Visual Studio 2015][1]
5. Klik met de rechtermuisknop Hallo **npm** uit en selecteer **installeren nieuwe npm pakketten...** .
6. Mogelijk moet u toorefresh hello npm catalogus over het maken van uw eerste Node.js-toepassing.  Klik op **vernieuwen** indien nodig.
7. Voer *apps van azure mobile* in het zoekvak Hallo.  Klik op Hallo **azure mobile apps 2.0.0** van het pakket en klik vervolgens op **pakket installeren**.

    ![Nieuwe npm pakketten installeren][2]
8. Klik op **Sluiten**.
9. Open Hallo *app.js* tooadd ondersteuning voor hello Azure Mobile Apps SDK.  Regel 6 at Hallo onderaan Hallo-bibliotheek in instructies vereisen, Hallo na code toevoegen:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    Andere instructies app.use toevoegen op ongeveer regel 27 na Hallo Hallo code te volgen:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Hallo-bestand opslaan.
10. Voer Hallo toepassing lokaal (hello API worden geleverd op http://localhost: 3000) of tooAzure publiceren.

### <a name="create-node-backend-portal"></a>Procedure: een Node.js-backend met hello Azure-portal maken
U kunt een rechts van de back-end voor mobiele App maken in Hallo [Azure-portal]. Kunt u Hallo volgende stappen of een client en server samen te met de volgende Hallo maken volgen [maken van een mobiele app](app-service-mobile-ios-get-started.md) zelfstudie. Hallo-zelfstudie bevat een vereenvoudigde versie van deze instructies en wordt aanbevolen voor bewijs van concept projecten.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Terug in Hallo *aan de slag* blade onder **maken van een tabel-API**, kies **Node.js** als uw **back-endtaal**.
Hallo selectievakje voor '**ik erken dat hiermee alle inhoud van site overschreven wordt.**', klikt u vervolgens op **takentabel maken**.

### <a name="download-quickstart"></a>Hoe: Download Hallo Node.js-back-end Quick Start CodeProject met Git
Wanneer u een back-end voor Node.js mobiele App maakt met behulp van de portal Hallo **snel starten** blade een Node.js-project is gemaakt voor u en geïmplementeerde tooyour site. U kunt de tabellen en API's toevoegen en bewerken van codebestanden voor Hallo Node.js back-end in de portal Hallo. U kunt ook verschillende extra toodownload Hallo back-end implementatieproject gebruiken zodat u kunt toevoegen of tabellen en API's wijzigen en vervolgens opnieuw Hallo-project publiceren. Zie voor meer informatie de [Implementatiehandleiding voor Azure App Service]. Hallo wordt volgende procedure een Git-opslagplaats toodownload Hallo Quick Start-projectcode.

1. Installeer Git als u dat nog niet hebt gedaan. Hallo stappen vereist tooinstall Git variëren tussen besturingssystemen. Zie [installeren Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) voor besturingssysteem-specifieke distributies en installatie-instructies.
2. Hallo stappen in [inschakelen Hallo App Service-app opslagplaats](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable Hallo Git-opslagplaats voor uw back-end-site, waardoor een notitie van Hallo implementatie gebruikersnaam en wachtwoord.
3. Hallo blade voor uw back-end voor de mobiele App Noteer Hallo **Git-kloon-URL** instelling.
4. Hallo uitvoeren `git clone` opdracht Hallo Git-kloon-URL, invoeren van het wachtwoord indien nodig, zoals in het volgende voorbeeld met:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Bladeren toolocal directory, die in het voorgaande voorbeeld Hallo /todolist, en u ziet dat projectbestanden zijn gedownload. Zoek Hallo `todoitem.json` bestand in Hallo `/tables` directory.  Dit bestand definieert machtigingen voor de tabel.  Hallo ook zoeken `todoitem.js` bestanden per Hallo dezelfde directory waarmee wordt gedefinieerd dat CRUD-bewerking voor de tabel Hallo scripts.
6. Nadat u wijzigingen tooproject bestanden aangebracht hebt, uitvoeren Hallo opdrachten tooadd, doorvoeren en vervolgens de wijzigingen toohello site uploaden te volgen:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Wanneer u nieuwe bestanden toohello project toevoegt, moet u eerst tooexecute hello `git add .` opdracht.

Telkens wanneer een nieuwe reeks doorvoeracties wordt doorgeschoven, toohello site opnieuw Hallo site wordt gepubliceerd.

### <a name="howto-publish-to-azure"></a>Hoe: uw Node.js-back-end-tooAzure publiceren
Microsoft Azure biedt veel mechanismen voor het publiceren van uw Azure App Service Mobile Apps Node.js-back-end voor hello Azure-service.  Deze omvatten gebruik geïntegreerd in Visual Studio-hulpprogramma's voor, opdrachtregelprogramma's en continue implementatie-opties op basis van broncodebeheer.  Zie voor meer informatie over dit onderwerp de [Implementatiehandleiding voor Azure App Service].

Azure App Service biedt specifiek advies voor Node.js-toepassing die u vóór de implementatie controleren moet:

* Hoe te[Hallo knooppunt versie opgeven]
* Hoe te[knooppunt-modules gebruiken]

### <a name="howto-enable-homepage"></a>Procedure: een startpagina van uw toepassing inschakelen
Veel toepassingen zijn een combinatie van web- en mobiele apps en Hallo ExpressJS framework, kunt u de twee toocombine facetten.  Soms echter, kunt u tooonly implementeren een mobiele-interface.  Het is nuttig tooprovide die een landingspagina pagina tooensure Hallo app-service actief is.  Geef uw eigen introductiepagina of de startpagina van een tijdelijke inschakelen.  een tijdelijke introductiepagina tooenable gebruiken Hallo tooinstantiate Azure Mobile Apps te volgen:

    var mobile = azureMobileApps({ homePage: true });

Als u deze optie beschikbaar wilt bij het ontwikkelen van lokaal, kunt u deze instelling tooyour toevoegen `azureMobile.js` bestand.

## <a name="TableOperations"></a>Tabelbewerkingen
Hallo apps van azure mobile Node.js Server SDK biedt mechanismen tooexpose gegevens opgeslagen in Azure SQL Database als een WebAPI tabellen.  Er zijn vijf operations beschikbaar.

| Bewerking | Beschrijving |
| --- | --- |
| GET-/tables/*tablename* |Alle records in de tabel Hallo ophalen |
| GET-/tables/*tablename*/:id |Ophalen van een bepaalde record in de tabel Hallo |
| POST /tables/*tablename* |Een record in de tabel Hallo maken |
| PATCH /tables/*tablename*/:id |Een record in de tabel Hallo bijwerken |
| DELETE /tables/*tablename*/:id |Een record in de tabel Hallo verwijderen |

Biedt ondersteuning voor deze WebAPI [OData] en breidt Hallo tabel schema toosupport [offline gegevenssynchronisatie].

### <a name="howto-dynamicschema"></a>Hoe: tabellen met behulp van een dynamische schema definiëren
Voordat een tabel kan worden gebruikt, moet worden gedefinieerd.  Tabellen kunnen worden gedefinieerd met een statische schema (Hallo developer definieert waar Hallo kolommen in Hallo schema) of dynamisch (Hallo SDK bepaalt waar Hallo schema op basis van binnenkomende aanvragen). Bovendien kunt Hallo ontwikkelaars bepaalde aspecten van Hallo WebAPI beheren door Javascript-code toohello definitie toe te voegen.

Als een best practice moet u elke tabel in een Javascript-bestand in Hallo tabellen directory definiëren en vervolgens de tabellen tables.import() methode tooimport hello gebruiken.  Basic-app-Hallo uitbreidt, zou Hallo app.js bestand worden aangepast:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Hallo-tabel in definiëren. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Tabellen dynamische schema standaard gebruikt.  tooturn uit dynamische schema instellen globaal Hallo App-instelling **MS_DynamicSchema** toofalse binnen hello Azure-portal.

U vindt een compleet voorbeeld in Hallo [todo-voorbeeld op GitHub].

### <a name="howto-staticschema"></a>Hoe: tabellen met behulp van een statische schema definiëren
U kunt expliciet Hallo kolommen tooexpose via Hallo WebAPI definiëren.  Hello die node.js-SDK voor apps van azure mobile voegt automatisch eventuele extra kolommen die vereist zijn voor offline synchronisatie toohello gegevenslijst die u opgeeft.  De Quick Start-clienttoepassingen vereisen bijvoorbeeld dat een tabel met twee kolommen: tekst (tekenreeks) en (een Booleaanse waarde) te voltooien.  
Hallo tabel kan worden gedefinieerd in Hallo tabel definitie JavaScript-bestand (te vinden in Hallo tabellen directory) als volgt:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Als u tabellen statisch definieert, moet u ook Hallo tables.initialize() methode toocreate Hallo-databaseschema aanroepen tijdens het opstarten.  Hallo tables.initialize() methode retourneert een [belofte] zodat de webservice Hallo dienen geen aanvragen voordat Hallo-database wordt geïnitialiseerd.

### <a name="howto-sqlexpress-setup"></a>Hoe: Gebruik SQL Express als gegevensopslag ontwikkeling op uw lokale computer
Hello Azure Mobile Apps Hallo AzureMobile Apps knooppunt SDK biedt drie opties voor die gegevens out of box Hallo: SDK biedt drie opties voor die gegevens out of box Hallo:

* Gebruik Hallo **geheugen** stuurprogramma-archief voor het voorbeeld van een niet-permanente tooprovide
* Gebruik Hallo **mssql** stuurprogramma tooprovide gegevensopslag SQL Express voor ontwikkeling
* Gebruik Hallo **mssql** stuurprogramma tooprovide een Azure SQL Database-gegevensarchief voor productie

Hello Azure Mobile Apps Node.js SDK maakt gebruik van Hallo [mssql Node.js pakket] tooestablish en gebruik van een verbinding tooboth SQL Express- en SQL-Database.  Dit pakket vereist dat u TCP-verbindingen op uw exemplaar van SQL Express inschakelen.

> [!TIP]
> Hallo geheugen stuurprogramma biedt geen een volledige set van opslagruimten voor het testen.  Als u uw back-end lokaal tootest wilt, we raden aan Hallo gebruik van een gegevensarchief SQL Express en Hallo mssql-stuurprogramma.
>
>

1. Download en installeer [Microsoft SQL Server 2014 Express].  Zorg ervoor dat u SQL Server 2014 Express Hallo met extra editie installeren.  Tenzij u expliciet ondersteuning voor 64-bits vereist, verbruikt Hallo 32-bits versie minder geheugen uitgevoerd.
2. Hallo SQL Server 2014 Configuration Manager worden uitgevoerd.

   1. Vouw Hallo **SQL Server-netwerkconfiguratie** knooppunt in het menu van Hallo links structuur.
   2. Klik op **protocollen voor SQLEXPRESS**.
   3. Met de rechtermuisknop op **TCP/IP** en selecteer **inschakelen**.  Klik op **OK** in Hallo pop-upvenster.
   4. Met de rechtermuisknop op **TCP/IP** en selecteer **eigenschappen**.
   5. Klik op Hallo **IP-adressen** tabblad.
   6. Hallo zoeken **IPAll** knooppunt.  In Hallo **TCP-poort** veld **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Klik op **OK**.  Klik op **OK** in Hallo pop-upvenster.
   8. Klik op **SQL Server-Services** in het menu van Hallo links structuur.
   9. Met de rechtermuisknop op **SQL Server (SQLEXPRESS)** en selecteer **opnieuw starten**
   10. Hallo SQL Server 2014 Configuration Manager te sluiten.
3. Voer Hallo SQL Server 2014 Management Studio en maak verbinding tooyour lokale exemplaar van SQL Express

   1. Met de rechtermuisknop op uw exemplaar in Object Explorer Hallo en selecteer **eigenschappen**
   2. Selecteer Hallo **beveiliging** pagina.
   3. Zorg ervoor dat Hallo **modus van SQL Server en Windows-verificatie** is geselecteerd
   4. Klik op **OK**

          ![Configure SQL Express Authentication][4]
   5. Vouw **beveiliging** > **aanmeldingen** in Object Explorer Hallo
   6. Met de rechtermuisknop op **aanmeldingen** en selecteer **New Login...**
   7. Typ een aanmeldingsnaam.  Selecteer **SQL Server-verificatie**.  Voer een wachtwoord, voert u Hallo hetzelfde wachtwoord in **wachtwoord bevestigen**.  Hallo-wachtwoord moet voldoen aan de complexiteitsvereisten van Windows.
   8. Klik op **OK**

          ![Add a new user tooSQL Express][5]
   9. Met de rechtermuisknop op uw nieuwe aanmelding en selecteer **eigenschappen**
   10. Selecteer Hallo **serverfuncties** pagina
   11. Controleer Hallo vak volgende toohello **dbcreator** serverfunctie
   12. Klik op **OK**
   13. Hallo SQL Server 2015 Management Studio sluiten

Zorg ervoor dat u records Hallo-gebruikersnaam en wachtwoord die u hebt geselecteerd.  Mogelijk moet u de aanvullende serverfuncties tooassign of machtigingen, afhankelijk van de vereisten van uw specifieke database.

Hallo Node.js-toepassing hello leest **SQLCONNSTR_MS_TableConnectionString** omgevingsvariabele voor Hallo-verbindingsreeks voor deze database.  U kunt deze variabele instellen in uw omgeving.  Bijvoorbeeld, kunt u PowerShell tooset deze omgevingsvariabele:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Toegang tot Hallo-database via een TCP/IP-verbinding en geef een gebruikersnaam en wachtwoord voor Hallo-verbinding.

### <a name="howto-config-localdev"></a>Hoe: uw project voor lokale ontwikkeling configureren
Azure Mobile Apps leest een JavaScript-bestand aangeroepen *azureMobile.js* van het lokale bestandssysteem Hallo.  Niet gebruiken in dit bestand tooconfigure hello Azure Mobile Apps SDK in productie - App-instellingen gebruiken in Hallo [Azure-portal] in plaats daarvan.  Hallo *azureMobile.js* bestand moet een configuratieobject exporteren.  meest voorkomende Hallo-instellingen zijn:

* Database-instellingen
* Instellingen voor diagnostische logboekregistratie
* Alternatieve CORS-instellingen

Een voorbeeld *azureMobile.js* bestand Hallo voorafgaand aan de database-instellingen volgt implementeren:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Het is raadzaam dat u toevoegt, *azureMobile.js* tooyour *.gitignore* bestand (of andere broncodebeheer bestand negeren) tooprevent wachtwoorden worden opgeslagen in de cloud Hallo.  Altijd productie-instellingen configureren in App-instellingen in Hallo [Azure-portal].

### <a name="howto-appsettings"></a>Procedure: App-instellingen voor uw mobiele App configureren
De meeste instellingen in Hallo *azureMobile.js* bestand hebben een equivalente App-instelling in Hallo [Azure-portal].  Hallo lijst tooconfigure na uw app in App-instellingen gebruiken:

| App-instelling | *azureMobile.js* instelling | Beschrijving | Geldige waarden |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |naam |Hallo-naam van Hallo-app |Tekenreeks |
| **MS_MobileLoggingLevel** |Logging.level |Minimale logboekniveau van berichten toolog |fout, waarschuwing, info, uitgebreid, foutopsporing, stom |
| **MS_DebugMode** |Fouten opsporen |In- of de foutopsporingsmodus uitschakelen |True, false |
| **MS_TableSchema** |Data.schema |Naam van de standaard schema voor de SQL-tabellen |tekenreeks (standaard: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |In- of de foutopsporingsmodus uitschakelen |True, false |
| **MS_DisableVersionHeader** |versie (set tooundefined) |Hallo X-ZUMO-Server-versie-header wordt uitgeschakeld |True, false |
| **MS_SkipVersionCheck** |skipversioncheck |Controle van versie Hallo van client-API wordt uitgeschakeld |True, false |

tooset een App-instelling:

1. Meld u bij toohello [Azure-portal].
2. Selecteer **alle resources** of **App Services** klik vervolgens op Hallo-naam van uw mobiele App.
3. Standaard wordt de blade instellingen Hallo geopend. Als dit niet zo is, klikt u op **instellingen**.
4. Klik op **toepassingsinstellingen** in algemene Hallo-menu.
5. Schuif toohello sectie App-instellingen.
6. Als uw app instelt, al bestaat, klikt u op Hallo van Hallo app tooedit Hallo waarde.
7. Als uw app-instelling niet bestaat, voert u Hallo App-instelling in het vak Hallo-sleutel en Hallo-waarde in het vak Hallo-waarde.
8. Nadat u voltooid zijn, klikt u op **opslaan**.

Het wijzigen van de meeste appinstellingen voor vereist service opnieuw opstarten.

### <a name="howto-use-sqlazure"></a>Procedure: SQL-Database gebruiken als uw gegevensarchief productie
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Met behulp van Azure SQL Database als gegevensopslag is identiek alle typen voor Azure App Service-toepassing. Als u dit nog niet hebt gedaan, volgt u deze stappen toocreate een back-end voor de mobiele App.

1. Meld u bij toohello [Azure-portal].
2. In hello linksboven Hallo-venster, klikt u op Hallo **+ nieuw** knop > **Web en mobiel** > **mobiele App**, Geef een naam op voor uw back-end voor de mobiele App.
3. In Hallo **resourcegroep** Voer Hallo dezelfde naam als uw app.
4. Hallo standaard App Service-abonnement is geselecteerd.  Als u toochange uw App Service-abonnement wenst, kunt u doen door te klikken op Hallo App Service Plan > **+ maken van nieuwe**.  Geef een naam op van de nieuwe App Service-abonnement Hallo en selecteer de juiste locatie.  Klik op Hallo prijscategorie en selecteer een geschikte prijscategorie voor Hallo-service. Selecteer **weergeven van alle** tooview meer opties, zoals prijzen **vrije** en **gedeelde**.  Nadat u de prijscategorie hebt geselecteerd, klikt u op Hallo **Selecteer** knop.  Terug in Hallo **App Service-abonnement** blade, klikt u op **OK**.
5. Klik op **Create**. Inrichting van een back-end voor de mobiele App kan een paar minuten duren.  Zodra het Hallo-backend voor mobiele Apps is ingericht, Hallo wordt geopend Hallo **instellingen** blade voor back-end van Hallo mobiele App.

Zodra de back-end van Hallo mobiele App is gemaakt, kunt u tooeither verbinding maken met een bestaande SQL-database tooyour backend voor mobiele Apps of maak een nieuwe SQL-database.  In deze sectie maken we een SQL-database.

> [!NOTE]
> Als u al een database in Hallo dezelfde locatie als back-end van Hallo mobiele app in plaats daarvan kunt u **gebruik een bestaande database** en selecteer vervolgens die database. Hallo-gebruik van een database op een andere locatie wordt niet aanbevolen vanwege de hogere latenties.
>
>

1. Klik in het Hallo nieuwe backend voor mobiele Apps, op **instellingen** > **mobiele App** > **gegevens** > **+ toevoegen**.
2. In Hallo **gegevensverbinding toevoegen** blade, klikt u op **SQL Database - vereiste instellingen configureren** > **een nieuwe database maken**.  Voer de naam van de Hallo van de nieuwe database Hallo in Hallo **naam** veld.
3. Klik op **Server**.  In Hallo **nieuwe server** blade, voer een unieke naam in Hallo **servernaam** veld en geef een geschikte **aanmeldgegevens van serverbeheerder** en **wachtwoord**.  Zorg ervoor dat **toestaan azure-services tooaccess server** is ingeschakeld.  Klik op **OK**.

    ![Een Azure SQL-Database maken][6]
4. Op Hallo **nieuwe database** blade, klikt u op **OK**.
5. Terug op Hallo **gegevensverbinding toevoegen** blade Selecteer **verbindingsreeks**, Voer Hallo aanmeldingsnaam en het wachtwoord die u hebt opgegeven bij het maken van Hallo-database.  Als u een bestaande database gebruikt, geeft u Hallo-aanmeldingsreferenties voor die database.  Nadat u hebt ingevoerd, klikt u op **OK**.
6. Terug op Hallo **gegevensverbinding toevoegen** blade opnieuw in en klikt u op **OK** toocreate Hallo-database.

<!--- END OF ALTERNATE INCLUDE -->

Maken van database Hallo kan enkele minuten duren.  Gebruik Hallo **meldingen** gebied toomonitor Hallo voortgang van Hallo-implementatie.  Voortgang niet totdat het Hallo-database is geïmplementeerd.  Zodra met succes is geïmplementeerd, wordt een verbindingsreeks voor Hallo SQL Database-exemplaar in uw mobiele back-end App-instellingen gemaakt.  U kunt deze appinstelling in Hallo zien **instellingen** > **toepassingsinstellingen** > **verbindingsreeksen**.

### <a name="howto-tables-auth"></a>Procedure: verificatie vereisen voor toegang tot tootables
Als u toouse App Service-verificatie met Hallo tabellen eindpunt wenst, moet u App Service-verificatie configureren in Hallo [Azure-portal] eerste.  Voor meer informatie over het configureren van verificatie in een Azure App Service, bekijken Hallo configuratiehandleiding voor de identiteitsprovider hello wilt toouse:

* [Hoe tooconfigure Azure Active Directory-verificatie]
* [Hoe tooconfigure Facebook-verificatie]
* [Hoe tooconfigure Google-verificatie]
* [Hoe Microsoft Authentication tooconfigure]
* [Hoe tooconfigure Twitter-verificatie]

Elke tabel heeft een access-eigenschap die gebruikt toocontrol access toohello-tabel worden kan.  Hallo volgende voorbeeld ziet u een statisch gedefinieerde tabel met de verificatie is vereist.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Hallo access-eigenschap kan duren voordat een van drie waarden

* *anonieme* geeft aan dat de clienttoepassing Hallo tooread gegevens zonder verificatie is toegestaan
* *geverifieerde* geeft aan dat de clienttoepassing Hallo verificatietoken voor een geldig met Hallo-aanvraag moet verzenden
* *uitgeschakeld* geeft aan dat deze tabel is uitgeschakeld

Als Hallo access-eigenschap gedefinieerd is, is niet-geverifieerde toegang toegestaan.

### <a name="howto-tables-getidentity"></a>Procedure: verificatie claims gebruiken met uw tabellen
U kunt instellen wanneer er verschillende claims die worden aangevraagd wanneer verificatie is ingesteld.  Deze claims zijn niet normaal gesproken beschikbaar via Hallo `context.user` object.  Maar ze kunnen worden opgehaald met Hallo `context.user.getIdentity()` methode.  Hallo `getIdentity()` methode retourneert een voorraad die wordt omgezet tooan-object.  Hallo-object is ingevoerd met de verificatiemethode (facebook, google, twitter, microsoftaccount of aad).

Als u verificatie van de Microsoft-Account en aanvraag Hallo e-mailadressen claim hebt ingesteld, kunt u bijvoorbeeld Hallo e-mailadres toohello record toevoegen Hello tabel controller te volgen:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee welke claims beschikbaar zijn, gebruikt u een web browser tooview hello `/.auth/me` eindpunt van uw site.

### <a name="howto-tables-disabled"></a>Hoe: Schakel toegang toospecific tabelbewerkingen
In de toevoeging tooappearing op Hallo tabel worden Hallo toegang eigenschap gebruikte toocontrol afzonderlijke bewerkingen.  Er zijn vier bewerkingen:

* *Lees* RESTful GET Hallo-bewerking op Hallo-tabel is
* *invoegen* hello RESTful POST-bewerking op Hallo-tabel is
* *bijwerken* hello RESTful PATCH bewerking is voor Hallo tabel
* *Verwijder* hello RESTful verwijderbewerking op Hallo-tabel is

Bijvoorbeeld, kunt u desgewenst tooprovide een alleen-lezen niet-geverifieerde tabel:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Hoe: Hallo-query die wordt gebruikt met tabelbewerkingen aanpassen
Een algemene vereiste voor tabelbewerkingen is tooprovide een beperkte weergave van Hallo-gegevens.  Bijvoorbeeld, kunt u desgewenst een tabel die is gecodeerd met Hallo geverifieerde gebruikers-ID dat kunt u alleen lezen of bijwerken van uw eigen records.  Hallo tabeldefinitie na biedt deze functionaliteit:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Bewerkingen die normaal gesproken een query uitvoeren hebben een queryeigenschap die u met een waar aanpassen kunt component. eigenschap Hallo-query is een [QueryJS] dat object gebruikte tooconvert een OData-query toosomething die gegevens back-end Hallo kan verwerken.  Eenvoudige gelijkheid gevallen (zoals Hallo voorafgaand aan een), kan een kaart worden gebruikt. U kunt ook specifieke SQL-componenten toevoegen:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Hoe: voorlopig verwijderen configureren in een tabel
Voorlopige verwijderingen worden records niet daadwerkelijk verwijderd.  In plaats daarvan markeren het als verwijderd in de database Hallo door in te stellen Hallo verwijderde kolom tootrue.  Hello Azure Mobile Apps SDK automatisch voorlopig verwijderde records worden verwijderd uit de resultaten tenzij Hallo Mobile Client SDK IncludeDeleted() gebruikt.  een tabel voor voorlopig verwijderen, tooconfigure ingesteld Hallo `softDelete` eigenschap in het definitiebestand voor Hallo tabel:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Een mechanisme voor het opschonen van records - vanuit een clienttoepassing, via een webtaak, Azure-functie of via een aangepaste API gebruiken, moet u instellen.

### <a name="howto-tables-seeding"></a>Procedure: de database met gegevens Seed
Wanneer u een nieuwe toepassing maakt, kunt u desgewenst tooseed een tabel met gegevens.  Dit kan worden uitgevoerd binnen Hallo tabel definitie JavaScript-bestand als volgt:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Seeding van de gegevens wordt alleen uitgevoerd wanneer Hallo tabel door hello Azure Mobile Apps SDK is gemaakt.  Als Hallo tabel al in Hallo-database bestaat, wordt er worden geen gegevens ingevoegd in Hallo tabel.  Als u dynamische schema is ingeschakeld, klikt u vervolgens het schema afgeleid van Hallo seeding gegevens.

Het is raadzaam dat u niet expliciet Hallo aanroepen `tables.initialize()` methode toocreate Hallo tabel Hallo-service wordt gestart.

### <a name="Swagger"></a>Hoe: Swagger-ondersteuning inschakelen
Azure App Service Mobile Apps wordt geleverd met ingebouwde [Swagger] ondersteunen.  Hallo swagger-ui tooenable Swagger-ondersteuning, eerst installeren als een afhankelijkheid:

    npm install --save swagger-ui

Zodra u hebt geïnstalleerd, kunt u ondersteuning voor Swagger in Azure Mobile Apps-constructor Hallo inschakelen:

    var mobile = azureMobileApps({ swagger: true });

U waarschijnlijk alleen wilt tooenable Swagger worden ondersteund in ontwikkeling edities.  U kunt dit doen door het gebruik van de `NODE_ENV` app-instelling:

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Hallo swagger-eindpunt bevindt zich op http://*uw site*.azurewebsites.net/swagger.  U hebt toegang tot Hallo Swagger-gebruikersinterface via Hallo `/swagger/ui` eindpunt.  Als u ervoor verificatie toorequire inlezen in uw hele toepassing kiest, Swagger, treedt een fout.  Kies voor de beste resultaten tooallow niet-geverifieerde aanvragen via in hello Azure App Service-verificatie / autorisatie-instellingen beheren vervolgens verificatie met behulp van Hallo `table.access` eigenschap.

U kunt ook toevoegen Hallo Swagger optie tooyour `azureMobile.js` als u alleen Swagger ondersteuning bij het ontwikkelen van lokaal bestand.

## <a name="a-namepushpush-notifications"></a><a name="push">Pushmeldingen
Mobiele Apps worden geïntegreerd met Azure Notification Hubs tooenable u toosend gericht push notifications toomillions van apparaten voor alle primaire platforms. U kunt pushmeldingen verzenden via Notification Hubs meldingen tooiOS, Android en Windows-apparaten. meer informatie over alles wat u kunt doen met toolearn Notification Hubs, Zie [overzicht van Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Hoe: pushmeldingen verzenden
Hallo volgende code toont hoe toouse Hallo push object toosend een uitzending push-melding tooregistered iOS-apparaten:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Door een sjabloon push-registratie van Hallo client maakt, kunt u in plaats daarvan een sjabloon push-bericht toodevices op alle ondersteunde platforms verzenden. Hallo van de volgende code wordt getoond hoe toosend een melding van de sjabloon:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Hoe: verzenden push notifications tooan geverifieerde gebruiker met tags
Wanneer een geverifieerde gebruiker geregistreerd voor pushmeldingen, wordt een gebruikers-ID-tag toohello registratie automatisch toegevoegd. Met deze code, kunt u push notifications tooall apparaten zijn geregistreerd door een specifieke gebruiker verzenden. Hallo volgende code wordt Hallo SID van gebruiker Hallo-aanvraag en verzendt een sjabloon tooevery apparaatregistratie voor pushberichten voor die gebruiker:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Wanneer u registreert voor pushmeldingen vanuit een geverifieerde client, moet u ervoor zorgen dat de verificatie is voltooid voordat u de registratie.

## <a name="CustomAPI"></a>Aangepaste API 's
### <a name="howto-customapi-basic"></a>Procedure: een aangepaste API definiëren
Bovendien toohello data access-API via Hallo /tables eindpunt, Azure Mobile Apps dekking van uw aangepaste API kan bieden.  Aangepaste API's worden gedefinieerd in een vergelijkbare manier toohello tabeldefinities en toegang tot alle Hallo dezelfde mogelijkheden, zoals verificatie.

Als u toouse App Service-verificatie met een aangepaste API wenst, moet u App Service-verificatie configureren in Hallo [Azure-portal] eerste.  Voor meer informatie over het configureren van verificatie in een Azure App Service, bekijken Hallo configuratiehandleiding voor de identiteitsprovider hello wilt toouse:

* [Hoe tooconfigure Azure Active Directory-verificatie]
* [Hoe tooconfigure Facebook-verificatie]
* [Hoe tooconfigure Google-verificatie]
* [Hoe Microsoft Authentication tooconfigure]
* [Hoe tooconfigure Twitter-verificatie]

Aangepaste API's zijn gedefinieerd op ongeveer dezelfde manier als tabellen API Hallo Hallo.

1. Maak een **api** directory
2. Het JavaScript-bestand van een API-definitie maken in Hallo **api** directory.
3. Gebruik Hallo importeren methode tooimport hello **api** directory.

Hier volgt Hallo prototype api-definitie op basis van Hallo basic-app voorbeeld die hebben we eerder hebt gebruikt.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Voorbeeld-API die retourneert Hallo server datum Hallo met *Date.now()* methode.  Hier volgt Hallo api/date.js bestand:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Elke parameter is een van de Hallo RESTful Standaardwerkwoorden - GET, POST, PATCH of verwijderen.  Hallo-methode is een standaard [ExpressJS Middleware] functie die u output Hallo vereist verzendt.

### <a name="howto-customapi-auth"></a>Procedure: verificatie vereisen voor toegang tot tooa aangepaste API
Azure Mobile Apps SDK wordt de verificatie geïmplementeerd in Hallo dezelfde manier voor zowel Hallo tabellen eindpunt en aangepaste API's.  Als u wilt toevoegen verificatie toohello API ontwikkeld in de vorige sectie hello, een **toegang** eigenschap:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

U kunt ook verificatie op specifieke bewerkingen opgeven:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Hallo moet hetzelfde token die wordt gebruikt voor het Hallo tabellen eindpunt worden gebruikt voor aangepaste API's waarvoor verificatie is vereist.

### <a name="howto-customapi-auth"></a>Hoe: grote bestandsuploads verwerken
Azure Mobile Apps SDK gebruikt Hallo [hoofdtekst parser middleware](https://github.com/expressjs/body-parser) tooaccept en inhoud van de hoofdtekst van de inzending decoderen.  U kunt vooraf hoofdtekst parser tooaccept groter bestandsuploads configureren:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Hallo-bestand is base 64-codering voor verzending.  Dit verhoogt de Hallo grootte van de werkelijke uploaden Hallo (en daarom moet u rekening houden met de grootte van Hallo).

### <a name="howto-customapi-sql"></a>Hoe: uitvoeren van aangepaste SQL-instructies
Hello Azure Mobile Apps SDK kunt u access toohello gehele Context via Hallo request-object, zodat u tooexecute geparametriseerde toohello gedefinieerde gegevensprovider voor SQL-instructies eenvoudig:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Foutopsporing, gemakkelijk tabellen en eenvoudige API 's
### <a name="howto-diagnostic-logs"></a>Procedure: fouten opsporen, diagnoses stellen en problemen met Azure Mobile apps
Hello Azure App Service biedt verschillende opsporen en oplossen van technieken voor Node.js-toepassingen.
Raadpleeg toohello artikelen tooget gestart bij het oplossen van uw back-end voor Node.js Mobile te volgen:

* [Bewaking van een Azure App Service]
* [Diagnostische logboekregistratie in Azure App Service inschakelen]
* [Een Azure App Service in Visual Studio oplossen]

Node.js-toepassingen toegang hebben tooa breed scala aan extra diagnostische logboeken.  Intern Hallo maakt gebruik van Azure Mobile Apps Node.js SDK [Winston] voor diagnostische logboekregistratie.  Logboekregistratie is standaard ingeschakeld door de foutopsporingsmodus inschakelen of Hallo instellen **MS_DebugMode** tootrue van app-instelling in Hallo [Azure-portal]. Gegenereerde logboeken worden weergegeven in Hallo diagnostische logboeken op Hallo [Azure-portal].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procedure: werken met gemakkelijk tabellen in hello Azure-portal
Eenvoudig tabellen in het Hallo-portal kunnen u maken en werken met tabellen rechts in Hallo-portal. U kunt zelfs tabelbewerkingen Hallo App Service-Editor met bewerken.

Wanneer u klikt op **gemakkelijk tabellen** in uw back-end voor site-instellingen kunt u toevoegen, wijzigen of verwijderen van een tabel. U ziet ook de gegevens in de tabel Hallo.

![Werken met gemakkelijk tabellen](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hallo zijn volgende opdrachten beschikbaar op de opdrachtbalk Hallo voor een tabel:

* **Machtigingen wijzigen** - wijzigen Hallo-machtiging voor lezen, invoegen, bijwerken en verwijderen van bewerkingen op Hallo tabel.
  Opties zijn tooallow anonieme toegang, toorequire verificatie of toodisable alle toegang tot toohello bewerking.
* **Bewerk script** -Hallo scriptbestand voor de tabel Hallo in Hallo App Service-Editor wordt geopend.
* **Schema beheren** - toevoegen of verwijderen van kolommen of Hallo tabelindex wijzigen.
* **Tabel wissen** -afgekapt van een bestaande tabel verwijderen van alle gegevensrijen maar waarbij Hallo schema ongewijzigd.
* **Verwijderen van rijen** -afzonderlijke rijen met gegevens te verwijderen.
* **Weergave streaminglogboeken** -u toohello streaming log-service voor uw site verbindt.

### <a name="work-easy-apis"></a>Procedure: werken met eenvoudige API's in hello Azure-portal
Eenvoudige API's in Hallo-portal kunt u maken en werken met aangepaste API's rechts in Hallo-portal. Hallo App Service-Editor met API-scripts, kunt u bewerken.

Wanneer u klikt op **eenvoudige API's** in uw back-end voor site-instellingen kunt u toevoegen, wijzigen of verwijderen van een aangepaste API-eindpunt.

![Werken met eenvoudige API 's](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

In Hallo-portal kunt u wijzigen Hallo toegangsmachtigingen voor een bepaalde HTTP-actie, scriptbestand Hallo-API in App Service Editor bewerken of Hallo streaminglogboeken weergeven.

### <a name="online-editor"></a>Hoe: code bewerken in Hallo App Service-Editor
Hello Azure-portal kunt u uw Node.js-back-end scriptbestanden in App Service-Editor Hallo bewerken zonder te hoeven Hallo project tooyour lokale computer downloaden. tooedit scriptbestanden in Hallo online-editor:

1. Klik op de blade van uw mobiele App-back-end **alle instellingen** > beide **gemakkelijk tabellen** of **eenvoudige API's**, klikt u op een tabel of de API en klik vervolgens op **script bewerken**. Hallo-scriptbestand wordt geopend in Hallo App Service-Editor.

    ![App Service-Editor](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Breng uw wijzigingen toohello code-bestand in Hallo online-editor. Wijzigingen worden automatisch opgeslagen terwijl u typt.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android Client Quick Start]: app-service-mobile-android-get-started.md
[Apache Cordova-Client Quick Start]: app-service-mobile-cordova-get-started.md
[iOS-Client Quick Start]: app-service-mobile-ios-get-started.md
[Quick Start voor Xamarin.iOS-Client]: app-service-mobile-xamarin-ios-get-started.md
[Snelstartgids voor Xamarin.Android-Client]: app-service-mobile-xamarin-android-get-started.md
[Quick Start Xamarin.Forms-Client]: app-service-mobile-xamarin-forms-get-started.md
[Windows Store-Client Quick Start]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[offline gegevenssynchronisatie]: app-service-mobile-offline-data-sync.md
[Hoe tooconfigure Azure Active Directory-verificatie]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Hoe tooconfigure Facebook-verificatie]: app-service-mobile-how-to-configure-facebook-authentication.md
[Hoe tooconfigure Google-verificatie]: app-service-mobile-how-to-configure-google-authentication.md
[Hoe Microsoft Authentication tooconfigure]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Hoe tooconfigure Twitter-verificatie]: app-service-mobile-how-to-configure-twitter-authentication.md
[Implementatiehandleiding voor Azure App Service]: ../app-service-web/web-sites-deploy.md
[Bewaking van een Azure App Service]: ../app-service-web/web-sites-monitor.md
[Diagnostische logboekregistratie in Azure App Service inschakelen]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Een Azure App Service in Visual Studio oplossen]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[Hallo knooppunt versie opgeven]: ../nodejs-specify-node-version-azure-apps.md
[knooppunt-modules gebruiken]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure-portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[belofte]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp voorbeeld op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo-voorbeeld op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directory voorbeelden op GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[1.1 van Node.js-hulpprogramma's voor Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js pakket]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
