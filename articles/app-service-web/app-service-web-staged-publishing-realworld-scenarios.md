---
title: DevOps-omgevingen effectief gebruiken voor uw web-app | Microsoft Docs
description: Informatie over het gebruik van implementatiesites instellen en beheren van meerdere ontwikkelomgevingen voor uw toepassing
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>DevOps-omgevingen effectief gebruiken voor uw web-apps
In dit artikel laat zien hoe instellen en beheren van implementaties van web application wanneer meerdere versies van uw toepassing zich in verschillende omgevingen zoals ontwikkeling, tijdelijke, kwaliteit assurance (QA) en productie. Elke versie van uw toepassing kan worden overwogen als een ontwikkelomgeving voor het specifieke doel van uw implementatie. Ontwikkelaars kunnen bijvoorbeeld de QA-omgeving gebruiken voor het testen van de kwaliteit van de toepassing voordat ze push de wijzigingen naar productie.
Meerdere ontwikkelomgevingen kunnen een uitdaging zijn, omdat u wilt bijhouden code, middelen (berekening, web-app, database, cache, enzovoort) beheren en code implementeren in omgevingen.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Instellen van een niet-productieomgeving (fase, Developer, QA)
Nadat een productie-web-app actief en werkend is, wordt de volgende stap is het maken van een niet-productieomgeving. Zorg dat u in de Standard of Premium Azure App Service plan-modus worden uitgevoerd voor het gebruik van implementatiesites. Implementatiesites zijn live web-apps die hun eigen hostnamen hebben. Web-app inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van de productiesite. Als u uw toepassing op een implementatiesleuf implementeert, krijgt u de volgende voordelen:

- U kunt wijzigingen in een web-app in een gefaseerde installatie implementatiesleuf valideren voordat het wisselen van de app met de productiesite.
- Wanneer u een WebApp in een sleuf eerst implementeren en deze in productie te wisselen, worden alle exemplaren van de sleuf zich vóór gewisseld naar de productie opgewarmd. Dit proces elimineert uitvaltijd wanneer u uw web-app implementeert. Het verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd omdat swap-bewerkingen. Configureren voor het automatiseren van deze volledige werkstroom [automatisch wisselen](web-sites-staged-publishing.md#configure-auto-swap) wanneer vooraf swap-validatie is niet nodig.
- Als een wisseling heeft de sleuf waarin de eerder voorbereide web-app nu is de vorige productie web-app. Als de gewisseld naar de productiesite wijzigingen zijn niet zoals u verwacht, kunt u de dezelfde swap uitvoeren onmiddellijk om uw web-'laatste bekende juiste configuratie' back-app.

Als u een gefaseerde installatie implementatiesleuf instelt, Zie [faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md). Elke omgeving moet een eigen set resources bevatten. Bijvoorbeeld, als uw web-app gebruikmaakt van een database, moeten klikt u vervolgens productie- en staging-web-apps gebruiken verschillende databases. Fasering ontwikkeling omgeving resources zoals database-, opslag- of -cache in te stellen uw ontwikkelomgeving staging toevoegen.

## <a name="examples-of-using-multiple-development-environments"></a>Voorbeelden van het gebruik van meerdere ontwikkelomgevingen
Elk project beheer van gegevensbronnen code met ten minste twee omgevingen moet volgen: ontwikkeling en productie. Als u content management systems (CMSs), App-frameworks, enz., ondersteunen de toepassing mogelijk niet in dit scenario zonder aanpassing. Dit deze is ingesteld op true voor een aantal van de gebruikte frameworks die in de volgende secties worden besproken. Groot aantal vragen keert naar rekening wanneer u met CMS/frameworks, zoals werkt:

- Hoe u de inhoud uit opdelen in verschillende omgevingen?
- Welke bestanden kunt u wijzigen zonder de framework-versie-updates
- Hoe beheert u configuraties per omgeving?
- Hoe beheert u versie-updates voor modules, invoegtoepassingen en het framework core?

Er zijn veel manieren voor het instellen van meerdere omgevingen voor uw project. De volgende voorbeelden ziet een methode voor elke betreffende toepassing.

### <a name="wordpress"></a>WordPress
In deze sectie leert u hoe u een werkstroom voor de implementatie met behulp van sleuven voor WordPress instelt. WordPress, zoals de meeste CMS-oplossingen, ondersteunt geen meerdere ontwikkelomgevingen zonder aanpassing. De functie Web Apps van Azure App Service heeft enkele functies om gemakkelijk voor het opslaan van configuratie-instellingen buiten uw code.

1. Voordat u een faseringssleuf maakt, kunt u instellen van uw toepassingscode ter ondersteuning van meerdere omgevingen. Ter ondersteuning van meerdere omgevingen in WordPress, moet u bewerken `wp-config.php` op uw lokale ontwikkel web-app en voeg de volgende code toe aan het begin van het bestand. Dit proces wordt uw toepassing om op te halen van de juiste configuratie op basis van de geselecteerde omgeving inschakelen.

    ```
    // Support multiple environments
    // set the config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. Maak een map onder de web-app root aangeroepen `config`, en voeg de `wp-config.azure.php` en `wp-config.local.php` bestanden die uw Azure-omgeving en de lokale omgeving respectievelijk vertegenwoordigen.

3. Kopieer de volgende in `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Instellen van de beveiliging sleutels zoals geïllustreerd in de vorige code helpen kunnen om te voorkomen dat uw web-app wordt gehackte unieke waarden dus gebruiken. Als u nodig hebt voor het genereren van de tekenreeks voor beveiligingssleutels vermeld in de code, kunt u [gaat u naar de automatische generator](https://api.wordpress.org/secret-key/1.1/salt) voor het maken van nieuwe sleutel/waarde-paren.

4. Kopieer de volgende code in `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Relatieve paden gebruiken
Een ding te configureren in de WordPress-app is relatieve paden. WordPress bevat gegevens van de URL in de database. Deze opslag maakt verplaatsen inhoud van de ene omgeving naar een andere moeilijker. U moet de database bijwerken telkens wanneer u van lokale naar werkgebied of fase naar productieomgevingen verplaatst. Om het risico van problemen die kunnen worden veroorzaakt bij de implementatie van een database telkens wanneer u van de ene omgeving naar een andere implementeren, gebruiken de [hoofdmap relatieve koppelingen invoegtoepassing](https://wordpress.org/plugins/root-relative-urls/), die u kunt installeren met behulp van het dashboard WordPress-beheerder.

De volgende items aan uw `wp-config.php` bestand voordat de `That's all, stop editing!` Opmerking:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Activeren van de invoegtoepassing via het `Plugins` menu in het dashboard voor WordPress-beheerder. Sla uw permalink-instellingen voor de WordPress-app.

#### <a name="the-final-wp-configphp-file"></a>De laatste `wp-config.php` bestand
Eventuele updates van de core WordPress heeft geen invloed op uw `wp-config.php`, `wp-config.azure.php`, en `wp-config.local.php` bestanden. Hier volgt een definitieve versie van de `wp-config.php` bestand:

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Een testomgeving instellen
1. Als u al een WordPress-web-app uitgevoerd op uw Azure-abonnement hebt, meld u bij de [Azure-portal](http://portal.azure.com), en gaat u naar uw WordPress-web-app. Als u een WordPress-web-app niet hebt, kunt u een vanuit Azure Marketplace. Zie voor meer informatie, [een WordPress-web-app maken in Azure App Service](web-sites-php-web-site-gallery.md).
Klik op **instellingen** > **implementatiesites** > **toevoegen** een implementatiesleuf te maken met de naam *fase* . Een implementatiesleuf is een andere webtoepassing die dezelfde bronnen als de primaire web-app die u eerder hebt gemaakt, deelt.

    ![Fase implementatiesleuf maken](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Toevoegen van een andere MySQL-database, spreek `wordpress-stage-db`, aan de resourcegroep `wordpressapp-group`.

    ![MySQL-database toevoegen aan resourcegroep](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Werk de verbindingsreeksen voor uw implementatiesleuf fase verwijzen naar de nieuwe database `wordpress-stage-db`. Uw web-app van productie `wordpressprodapp`, en web-app voor fasering `wordpressprodapp-stage`, moet verwijzen naar andere databases.

#### <a name="configure-environment-specific-app-settings"></a>Omgeving-specifieke app-instellingen configureren
Ontwikkelaars kunnen sleutel-waardeparen tekenreeks opslaan in Azure als onderdeel van de configuratie-informatie, aangeroepen **Appinstellingen**, die is gekoppeld aan een web-app. Tijdens runtime, web-apps automatisch deze waarden ophaalt en beschikbaar stellen aan code die wordt uitgevoerd in uw web-app. Vanuit het beveiligingsoogpunt van die een voordeel nice aan clientzijde is omdat vertrouwelijke gegevens, zoals databaseverbindingsreeksen wachtwoorden, waaronder nooit worden weergegeven als leesbare tekst in een bestand, zoals `wp-config.php`.

Dit proces wordt uitgelegd in de volgende leden, is nuttig omdat het omvat zowel bestandswijzigingen en wijzigingen in de database voor de WordPress-app:

* Upgrade van de WordPress-versie
* Nieuwe toevoegen of bewerken of upgraden van invoegtoepassingen
* Nieuwe toevoegen of bewerken of upgraden van thema 's

Configureer appinstellingen voor:

* Database-informatie
* In- en uitgeschakeld WordPress logboekregistratie inschakelen
* WordPress-beveiligingsinstellingen

![App-instellingen voor Wordpress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Zorg ervoor dat u de volgende appinstellingen voor uw web-app en fase productiesite toevoegt. Houd er rekening mee dat de web-app voor productie en fasering web-app gebruikmaken van verschillende databases.

1. Schakel de **sleuf instelling** selectievakjes uit voor alle instellingen-parameters behalve WP_ENV. Dit proces wordt wisselen van de configuratie voor uw web-app, de inhoud van bestanden en de database. Als **sleuf instelling** is ingeschakeld, de app-instellingen en de verbinding van de web-app string configuratie wordt *niet* verplaatsen tussen omgevingen bij het uitvoeren van een **wisselen** bewerking. Alle databasewijzigingen die aanwezig zijn, worden uw productie-web-app niet verbroken.

2. De ontwikkeling van lokale omgeving web-app implementeren op de fase web-app en de database met WebMatrix of hulpprogramma's van uw keuze, zoals FTP, Git of PhpMyAdmin.

    ![Web Matrix publiceren dialoogvenster voor WordPress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Bladeren en test uw tijdelijke web-app. In overweging een scenario waarbij het thema van de web-app worden bijgewerkt, is dit de tijdelijke web-app.

    ![Tijdelijke web-app bladeren voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Als alle er goed uitziet, klikt u op de **wisselen** knop op uw web-app Test uw inhoud verplaatsen naar de productieomgeving. In dit geval u de web-app en de database wisselen tussen omgevingen tijdens elke **wisselen** bewerking.

    ![Voorbeeld van wijzigingen voor WordPress wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Als uw scenario moet alleen push-bestanden (Er zijn geen updates van de database), moet u controleren **sleuf instelling** voor alle de database-gerelateerde *appinstellingen* en *verbinding tekenreeksen instellingen* in de **Web-Appinstellingen** blade binnen de Azure-portal eerst de **wisselen**. In dit geval DB_NAME, DB_HOST DB_PASSWORD, DB_USER en standaardinstellingen voor verbinding tekenreeks mag niet weergegeven in voorbeeld van wijzigingen Als u dit doet een **wisselen**. Op dit moment kunt u wanneer de **wisselen** bewerking, de WordPress-web-app heeft alleen de updatebestanden.
    >
    >

    Eerst een **wisselen**, hier is de productie WordPress-web-app.
    ![Web-app voor productie voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Na de **wisselen** bewerking, het thema is bijgewerkt op uw web-app voor productie.

    ![Web-app voor productie na sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Als u terugdraaien wilt, gaat u naar het web productie **App-instellingen**, en klik op de **wisselen** knop wisselen van de web-app en de database van de productie te faseringssleuf gewisseld. Vergeet niet dat als wijzigingen in de database zijn opgenomen in een **wisselen** bewerking, klikt u vervolgens de volgende keer dat u voor uw tijdelijke web-app implementeert, moet u wijzigingen in de database voor de huidige database voor uw tijdelijke web-app implementeren. De huidige database is mogelijk de vorige productiedatabase of de fase-database.

#### <a name="summary"></a>Samenvatting
Hier volgt een algemene proces voor alle toepassingen die database heeft:

1. Installeer de toepassing op uw lokale omgeving.
2. Omgeving-specifieke configuraties (lokale en Azure Web Apps) bevatten.
3. Stel uw fasering en productie-omgevingen voor Web-Apps.
4. Als u een productietoepassing die al wordt uitgevoerd op Azure hebt, synchroniseert uw productie-inhoud (bestanden/code en database) naar de lokale en staging-omgevingen.
5. Uw toepassing ontwikkelen op uw lokale omgeving.
6. Plaats uw productie-web-app of vergrendelde modus en inhoud van de database van de productie naar faserings- en Developer-omgevingen te synchroniseren.
7. Implementeer aan de staging-omgeving en de test.
8. Implementeren naar productieomgeving.
9. Herhaal stap 4 tot en met 6.

### <a name="umbraco"></a>Umbraco
In deze sectie leert u hoe de Umbraco CMS een aangepaste module gebruikt om te implementeren in omgevingen met meerdere DevOps. In dit voorbeeld bevat een andere benadering voor het beheren van meerdere ontwikkelomgevingen.

[Umbraco CMS](http://umbraco.com/) is een populair .NET CMS-oplossing die wordt gebruikt door veel ontwikkelaars. Biedt de [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module voor het implementeren van ontwikkeling voor fasering naar productieomgevingen. U kunt gemakkelijk een lokale ontwikkelingsomgeving voor een Umbraco CMS-web-app maken met behulp van Visual Studio of WebMatrix.

- [Een Umbraco web-app maken met Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Een Umbraco web-app maken met WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Vergeet verwijderen van de `install` map onder uw toepassing en nooit naar werkgebied of productie web-apps te uploaden. Deze zelfstudie wordt WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Een testomgeving instellen
1. Maak een implementatiesleuf zoals eerder vermeld voor de webtoepassing Umbraco CMS, ervan uitgaande dat u hebt al een web-app Umbraco CMS up en wordt uitgevoerd. Als u dit niet doet, kunt u een van de Marketplace.
2. Bijwerken van de verbindingsreeks voor de implementatiesleuf fase verwijzen naar de nieuwe **umbraco-fase-db** database. Uw productie-web-app (umbraositecms-1) en het tijdelijke web-app (umbracositecms-1-fase) *moet* verwijzen naar andere databases.

    ![Bijwerken van de verbindingsreeks voor de web-app met nieuwe faseringsdatabase fasering](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Klik op **ophalen publicatie-instellingen** voor de implementatiesleuf **fase**. Dit proces zal een instellingenbestand publiceren met de gegevens die Visual Studio of WebMatrix nodig heeft om uw toepassing publiceren vanuit de lokale ontwikkeling web-app in de Azure-web-app downloaden.

    ![Get-instelling van de tijdelijke web-app publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Open uw web-app voor lokale ontwikkeling in WebMatrix of Visual Studio. Deze zelfstudie wordt WebMatrix. U moet eerst de publish settings-bestand voor uw tijdelijke web-app importeren.

    ![Publicatie-instellingen voor Umbraco met behulp van Web Matrix importeren](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Controleer de wijzigingen in het dialoogvenster en uw lokale web-app implementeren in uw Azure-web-app *umbracositecms-1-fase*. Wanneer u bestanden rechtstreeks naar uw tijdelijke web-app implementeert, wordt u weglaten bestanden in de `~/app_data/TEMP/` map omdat deze bestanden worden opnieuw gegenereerd wanneer de fase web-app eerst gestart. U moet ook weglaten de `~/app_data/umbraco.config` -bestand, dat ook worden opnieuw gegenereerd.

    ![Controleer de wijzigingen publiceren in web matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Nadat u de Umbraco lokale web-app is gepubliceerd naar de tijdelijke web-app, blader naar uw tijdelijke web-app en enkele tests sprake is van eventuele problemen uitvoeren.

#### <a name="set-up-the-courier2-deployment-module"></a>De module Courier2 implementatie instellen
Met de [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, u kunt gewoon met de rechtermuisknop op push-inhoud, opmaakmodellen en modules voor ontwikkeling van een tijdelijke web-app in een productie-web-app. Dit proces vermindert het risico van uw web-app voor productie wanneer u een update implementeert op te splitsen.
Schaf een licentie voor Courier2 voor de `*.azurewebsites.net` en uw aangepaste domein (bijvoorbeeld http://abc.com). Nadat u de licentie koopt, plaatst u de gedownloade licentie (. LIC-bestand) in de `bin` map.

![Licentiebestand onder de bin-map verwijderen](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Download het pakket Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Aanmelden bij uw fase web-app spreek http://umbracocms-site-stage.azurewebsites.net/umbraco, klikt u op de **Developer** menu en klik vervolgens op **pakketten** > **lokaal installeren pakket**.

    ![Het installatieprogramma Umbraco-pakket](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Upload het pakket Courier2 met behulp van het installatieprogramma.

    ![Pakket voor courier module uploaden](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. Voor het configureren van het pakket dat u wilt bijwerken van het bestand courier.config onder de **Config** map van uw web-app.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Onder `<repositories>`, geef de URL en de gebruiker-informatie voor de site voor productie.
    Als u de standaardprovider Umbraco-lidmaatschap gebruikt, voegt u de ID voor de beheer-gebruiker in de &lt;gebruiker&gt; sectie.
    Als u een aangepaste Umbraco lidmaatschapsprovider, gebruikt u `<login>`,`<password>` in de module Courier2 verbinding maken met de productiesite.
    Voor meer informatie [Raadpleeg de documentatie voor de module Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Op dezelfde manier de Courier2-module installeren op uw productiesite, en configureer deze om te verwijzen naar de web-app voor de fase in het bestand van de respectieve courier.config zoals hier wordt weergegeven.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Klik op de **Courier2** tabblad in het dashboard Umbraco CMS web app en klik vervolgens op **locaties**. U ziet de naam van de opslagplaats op zoals vermeld in `courier.config`. Doe dit proces op uw productie- en staging-web-apps.

    ![Weergave bestemming web-app-opslagplaats](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. Ga voor het implementeren van inhoud van de staging-site naar de productiesite naar **inhoud**, en selecteer een bestaande pagina of maak een nieuwe pagina. Ik selecteer een bestaande pagina Mijn web-app waarin de titel van de pagina is **aan de slag: nieuwe**, en klik vervolgens op **opslaan en publiceren**.

    ![Titel van pagina wijzigen en publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Met de rechtermuisknop op de gewijzigde pagina om alle opties weer te geven. Klik op **Courier** openen de **implementatie** in het dialoogvenster. Klik op **implementeren** implementatie te starten.

    ![Dialoogvenster voor Courier module-implementatie](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Controleer de wijzigingen en klik vervolgens op **doorgaan**.

    ![Courier module implementatie dialoogvenster wijzigingen](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Het implementatielogboek bevat als de implementatie geslaagd is.

     ![Logboeken van de implementatie van Courier module weergeven](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Blader uw productie-web-app om te zien als de wijzigingen worden doorgevoerd.

     ![Productie web-app bladeren](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

Raadpleeg de documentatie voor meer informatie over het gebruik van Courier.

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a>Het bijwerken van de Umbraco CMS-versie
Courier wordt niet help u een upgrade van één versie van Umbraco CMS naar een andere uitvoert. Wanneer u een Umbraco CMS-versie bijwerkt, moet u controleren voor incompatibel zijn met uw aangepaste modules of modules van partners en de Umbraco Core-bibliotheken. Hier vindt u aanbevolen procedures:

* Maak altijd een back-up van uw web-app en database voordat u een upgrade. Op web-apps in Azure, kunt u automatische back-ups instellen voor uw websites met behulp van de back-up en herstellen van uw site indien nodig met behulp van de functie voor het terugzetten. Zie voor meer informatie [reservekopie maken van uw web-app](web-sites-backup.md) en [het herstellen van uw web-app](web-sites-restore.md).
* Controleer of de pakketten van partners compatibel met de versie die u een uitvoert zijn naar upgrade. Pagina voor het pakket te downloaden, controleert u de compatibiliteit van het project met Umbraco CMS-versie.

Voor meer informatie over het bijwerken van uw web-app lokaal [raadpleegt u de algemene upgraderichtlijnen](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Na de upgrade van uw lokale ontwikkelingssite publiceert u de wijzigingen aan de staging-web-app. Uw toepassing testen. Als alle er goed uitziet, gebruikt u de **wisselen** knop wisselen van de staging-site naar de productie-web-app. Wanneer u gebruikt de **wisselen** bewerking, kunt u de wijzigingen die worden beïnvloed weergeven in uw web-app-configuratie. Dit **wisselen** bewerking wisselt de web-apps en -databases. Na de **wisselen**, de productie-web-app verwijst naar de database umbraco-fase-db en het tijdelijke web-app verwijst naar umbraco-prod-db-database.

![Voorbeeld voor het implementeren van Umbraco CMS wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Hier volgen de voordelen van het wisselen van zowel de web-app als de database:

* U kunt terugkeren naar de vorige versie van uw web-app met een andere **wisselen** als er toepassingsproblemen zijn.
* Voor een upgrade moet u voor het implementeren van bestanden en de databases van de tijdelijke web-app in de web-app voor productie en de database. Groot aantal dingen kunnen fout gaan wanneer u bestanden en databases implementeert. Met behulp van de **wisselen** functie sleuven, we kunnen de uitvaltijd beperken tijdens een upgrade en vermindert het risico van fouten die zich voordoen kunnen bij het implementeren van wijzigingen.
* U kunt doen **A / B-tests** met behulp van de [testen in productie](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) functie.

In dit voorbeeld ziet u de flexibiliteit van het platform waarop u aangepaste modules die vergelijkbaar is met de module voor het beheren van de implementatie in omgevingen Umbraco Courier kunt samenstellen.

## <a name="references"></a>Verwijzingen
[Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)

[Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)

[Het blokkeren van webtoegang tot niet-productieve implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
