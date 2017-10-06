---
title: aaaUse DevOps omgevingen effectief voor uw web-app | Microsoft Docs
description: Meer informatie over hoe implementatie toouse tooset sleuven en het beheren van meerdere ontwikkelomgevingen voor uw toepassing
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
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>DevOps-omgevingen effectief gebruiken voor uw web-apps
Dit artikel ziet u hoe tooset en beheren van implementaties van web application wanneer meerdere versies van uw toepassing zich in verschillende omgevingen zoals ontwikkeling, tijdelijke, kwaliteit assurance (QA) en productie. Elke versie van uw toepassing kan worden overwogen als een ontwikkelomgeving voor Hallo specifiek doel van uw implementatie. Ontwikkelaars kunnen bijvoorbeeld Hallo QA omgeving tootest Hallo kwaliteit van de toepassing hello gebruiken voordat ze Hallo wijzigingen tooproduction push.
Meerdere ontwikkelomgevingen kunnen worden een uitdaging omdat u nodig hebt tootrack code, middelen (berekening, web-app, database, cache, enzovoort) beheren en implementeren van code in omgevingen.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Instellen van een niet-productieomgeving (fase, Developer, QA)
Nadat een productie-web-app actief en werkend is, is de volgende stap Hallo toocreate een niet-productieomgeving. toouse implementatiesites, zorg ervoor dat u in de modus voor Hallo Standard of Premium Azure App Service-abonnement worden uitgevoerd. Implementatiesites zijn live web-apps die hun eigen hostnamen hebben. Web-app inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van Hallo productiesite. Wanneer u uw toepassing tooa-implementatiesleuf implementeert, kunt u krijgen Hallo volgende voordelen:

- U kunt wijzigingen tooa web-app in een gefaseerde installatie implementatiesleuf valideren voordat u Hallo-app met de productiesite Hallo wisselen.
- Wanneer u een web-appsite tooa eerst implementeren en deze in productie te wisselen, worden alle exemplaren van Hallo sleuf zich vóór gewisseld naar de productie opgewarmd. Dit proces elimineert uitvaltijd wanneer u uw web-app implementeert. Hallo verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd vanwege tooswap bewerkingen. tooautomate deze volledige werkstroom configureren [automatisch wisselen](web-sites-staged-publishing.md#configure-auto-swap) wanneer vooraf swap-validatie is niet nodig.
- Als een wisseling heeft Hallo sleuf met Hallo eerder tijdelijke web-app nu Hallo vorige productie web-app. Als gewisseld naar de productiesite Hallo Hallo-wijzigingen zijn niet zoals u verwacht, kunt u Hallo uitvoeren dezelfde wisselen onmiddellijk tooget uw 'laatst bekende goede' web-app back.

Zie tooset van een gefaseerde installatie implementatiesleuf [faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md). Elke omgeving moet een eigen set resources bevatten. Bijvoorbeeld, als uw web-app gebruikmaakt van een database, moeten klikt u vervolgens productie- en staging-web-apps gebruiken verschillende databases. Fasering development environment resources, zoals database-, opslag- of cache tooset uw ontwikkelomgeving staging toevoegen.

## <a name="examples-of-using-multiple-development-environments"></a>Voorbeelden van het gebruik van meerdere ontwikkelomgevingen
Elk project beheer van gegevensbronnen code met ten minste twee omgevingen moet volgen: ontwikkeling en productie. Als u content management systems (CMSs), App-frameworks, enz., ondersteunen Hallo toepassing mogelijk niet in dit scenario zonder aanpassing. Dit deze is ingesteld op true voor een aantal Hallo populaire frameworks die worden besproken in Hallo uit te voeren. Groot aantal vragen horen toomind wanneer u met CMS/frameworks, zoals werkt:

- Hoe u uitsplitsing Hallo inhoud in verschillende omgevingen?
- Welke bestanden kunt u wijzigen zonder de framework-versie-updates
- Hoe beheert u configuraties per omgeving?
- Hoe beheert u versie-updates voor modules, invoegtoepassingen en Hallo basisschema?

Er zijn veel manieren tooset meerdere omgevingen voor uw project. Hallo volgende voorbeelden ziet u een methode voor elke betreffende toepassing.

### <a name="wordpress"></a>WordPress
In deze sectie leert u hoe tooset u een implementatiewerkstroom met behulp van WordPress sleuven. WordPress, zoals de meeste CMS-oplossingen, ondersteunt geen meerdere ontwikkelomgevingen zonder aanpassing. functie voor Hallo-Web-Apps van Azure App Service heeft een aantal functies waarmee u eenvoudig toostore configuratie-instellingen buiten uw code.

1. Voordat u een faseringssleuf maken, instellen van uw toepassing code toosupport omgevingen met meerdere. toosupport omgevingen met meerdere in WordPress, moet u tooedit `wp-config.php` op uw lokale ontwikkel web-app en het toevoegen van de volgende code aan begin van bestand Hallo HALLO hallo. Dit proces wordt uw toepassing toopick Hallo juiste configuratie inschakelen op basis van geselecteerde Hallo-omgeving.

    ```
    // Support multiple environments
    // set hello config file based on current environment
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
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Maak een map onder de web-app root aangeroepen `config`, en voeg Hallo `wp-config.azure.php` en `wp-config.local.php` bestanden die uw Azure-omgeving en de lokale omgeving respectievelijk vertegenwoordigen.

3. Kopieer de volgende Hallo in `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
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

    Hallo-beveiligingssleutels instellen, zoals geïllustreerd in de vorige code Hallo kunt tooprevent uw web-app van gehackte wordt gebruik helpen, dus unieke waarden. Als u toogenerate Hallo tekenreeks voor beveiligingssleutels vermeld in Hallo code nodig hebt, kunt u [Ga toohello automatische generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate nieuwe sleutel/waarde-paren.

4. Kopiëren Hallo volgende code in `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

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
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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
Een laatste ding tooconfigure in Hallo WordPress-app is relatieve paden. WordPress bevat gegevens van de URL in Hallo-database. Deze opslag is zwevend inhoud van de ene omgeving tooanother moeilijker. Tooupdate hello database moet u elke keer dat u verplaatst van de lokale toostage of fase tooproduction omgevingen. tooreduce hello risico van problemen die kunnen worden veroorzaakt bij de implementatie van een database telkens wanneer u vanaf de ene omgeving tooanother, gebruik Hallo implementeren [hoofdmap relatieve koppelingen invoegtoepassing](https://wordpress.org/plugins/root-relative-urls/), die u kunt installeren met behulp van Hallo WordPress-beheerder dashboard.

Hallo vermeldingen tooyour na toevoegen `wp-config.php` voordat Hallo `That's all, stop editing!` Opmerking:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Hallo-invoegtoepassing via Hallo activeren `Plugins` menu in het dashboard voor WordPress-beheerder. Sla uw permalink-instellingen voor de WordPress-app.

#### <a name="hello-final-wp-configphp-file"></a>Hallo laatste `wp-config.php` bestand
Eventuele updates van de core WordPress heeft geen invloed op uw `wp-config.php`, `wp-config.azure.php`, en `wp-config.local.php` bestanden. Hier volgt een definitieve versie van Hallo `wp-config.php` bestand:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Een testomgeving instellen
1. Als u al een WordPress-web-app uitgevoerd op uw Azure-abonnement hebt, meld u aan toohello [Azure-portal](http://portal.azure.com), en ga tooyour WordPress-web-app. Als u een WordPress-web-app niet hebt, kunt u een van de hello Azure Marketplace. toolearn meer, Zie [een WordPress-web-app maken in Azure App Service](web-sites-php-web-site-gallery.md).
Klik op **instellingen** > **implementatiesites** > **toevoegen** toocreate een implementatiesleuf met de naam van de Hallo *fase*. Een implementatiesleuf is een andere webtoepassing die shares Hallo dezelfde bronnen als Hallo primaire web-app die u eerder hebt gemaakt.

    ![Fase implementatiesleuf maken](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Toevoegen van een andere MySQL-database, spreek `wordpress-stage-db`, tooyour resourcegroep, `wordpressapp-group`.

    ![MySQL-database tooresource groep toevoegen](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Hallo-verbindingstekenreeksen voor de fase implementatiesleuf toopoint toohello nieuwe database maken, bijwerken `wordpress-stage-db`. Uw web-app van productie `wordpressprodapp`, en web-app voor fasering `wordpressprodapp-stage`, moet punt toodifferent databases.

#### <a name="configure-environment-specific-app-settings"></a>Omgeving-specifieke app-instellingen configureren
Ontwikkelaars kunnen sleutel-waardeparen tekenreeks opslaan in Azure als onderdeel van de configuratiegegevens hello, aangeroepen **Appinstellingen**, die is gekoppeld aan een web-app. Tijdens runtime, web-apps automatisch deze waarden ophaalt en zodat ze beschikbaar toocode die in uw web-app wordt uitgevoerd. Vanuit het beveiligingsoogpunt van die een voordeel nice aan clientzijde is omdat vertrouwelijke gegevens, zoals databaseverbindingsreeksen wachtwoorden, waaronder nooit worden weergegeven als leesbare tekst in een bestand, zoals `wp-config.php`.

Dit proces wordt uitgelegd in Hallo na alinea's, is nuttig omdat het omvat zowel bestandswijzigingen en wijzigingen in de database voor Hallo WordPress-app:

* Upgrade van de WordPress-versie
* Nieuwe toevoegen of bewerken of upgraden van invoegtoepassingen
* Nieuwe toevoegen of bewerken of upgraden van thema 's

Configureer appinstellingen voor:

* Database-informatie
* In- en uitgeschakeld WordPress logboekregistratie inschakelen
* WordPress-beveiligingsinstellingen

![App-instellingen voor Wordpress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Zorg ervoor dat u de volgende app-instellingen voor uw web-app en fase productiesite Hallo toevoegt. Houd er rekening mee dat Hallo productie web-app en fasering web-app verschillende databases gebruiken.

1. Schakel Hallo **sleuf instelling** selectievakjes uit voor alle parameters van Hallo instellingen behalve WP_ENV. Dit proces wordt Hallo configuratie wisselen voor uw web-app, de inhoud van bestanden en de database. Als **sleuf instelling** is dit selectievakje inschakelt, de app-instellingen en configuratie van de tekenreeks verbinding Hallo van web-app wordt *niet* verplaatsen tussen omgevingen bij het uitvoeren van een **wisselen** bewerking. Alle databasewijzigingen die aanwezig zijn, worden uw productie-web-app niet verbroken.

2. Hallo lokale ontwikkeling omgeving web app toohello fase web-app en database met WebMatrix of hulpprogramma's van uw keuze, zoals FTP, Git of PhpMyAdmin implementeren.

    ![Web Matrix publiceren dialoogvenster voor WordPress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Bladeren en test uw tijdelijke web-app. In overweging een scenario waarbij Hallo thema van web-app Hallo toobe bijgewerkt, moet u hier Hallo staging-web-app is.

    ![Tijdelijke web-app bladeren voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Als alle er goed uitziet, klikt u op Hallo **wisselen** knop op uw tijdelijke web-app toomove uw inhoud toohello productie-omgeving. In dit geval u Hallo WebApp en database Hallo wisselen tussen omgevingen tijdens elke **wisselen** bewerking.

    ![Voorbeeld van wijzigingen voor WordPress wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Als uw scenario moet tooonly push-bestanden (Er zijn geen updates van de database), moet u controleren **sleuf instelling** voor alle Hallo Databasegerelateerde *appinstellingen* en *verbinding tekenreeksen instellingen*in Hallo **Web-Appinstellingen** blade binnen hello Azure-portal voordat u Hallo **wisselen**. In dit geval DB_NAME, DB_HOST DB_PASSWORD, DB_USER en standaardinstellingen voor verbinding tekenreeks mag niet weergegeven in voorbeeld van wijzigingen Als u dit doet een **wisselen**. Op dit moment, wanneer u Hallo voltooid **wisselen** bewerking, wordt een WordPress-web-app hebt Hallo Hallo alleen bestanden worden bijgewerkt.
    >
    >

    Eerst een **wisselen**, hier is Hallo productie WordPress-web-app.
    ![Web-app voor productie voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Na het Hallo **wisselen** bewerking, Hallo thema is bijgewerkt op uw web-app voor productie.

    ![Web-app voor productie na sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Wanneer u tooroll weer nodig hebt, gaat u toohello productie web **Appinstellingen**, en klik op Hallo **wisselen** tooswap Hallo web-app en database uit productiesleuf toostaging knop. Vergeet niet dat als wijzigingen in de database zijn opgenomen in een **wisselen** bewerking en vervolgens Hallo volgende keer dat u implementeert tooyour staging-web-app, moet u toodeploy Hallo database wijzigingen toohello huidige database voor uw tijdelijke web-app. de huidige database Hallo mogelijk Hallo vorige productie of Hallo fase van de database.

#### <a name="summary"></a>Samenvatting
Hier volgt een algemene proces voor alle toepassingen die database heeft:

1. Hallo-toepassing installeren op uw lokale omgeving.
2. Omgeving-specifieke configuraties (lokale en Azure Web Apps) bevatten.
3. Stel uw fasering en productie-omgevingen voor Web-Apps.
4. Als u een productietoepassing die al wordt uitgevoerd op Azure hebt, synchroniseert u uw inhoud (bestanden/code en database) toolocal en fasering productieomgevingen.
5. Uw toepassing ontwikkelen op uw lokale omgeving.
6. Plaats uw productie-web-app of vergrendelde modus en inhoud van de database van toostaging en dev productieomgevingen synchroniseren.
7. Implementeer toohello staging-omgeving en testen.
8. Tooproduction omgeving implementeren.
9. Herhaal stap 4 tot en met 6.

### <a name="umbraco"></a>Umbraco
In deze sectie leert u hoe Hallo Umbraco CMS maakt gebruik van een aangepaste module toodeploy tussen meerdere DevOps-omgevingen. In dit voorbeeld bevat een andere benadering toomanaging meerdere ontwikkelomgevingen.

[Umbraco CMS](http://umbraco.com/) is een populair .NET CMS-oplossing die wordt gebruikt door veel ontwikkelaars. Het biedt Hallo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy van ontwikkelomgevingen toostaging tooproduction. U kunt gemakkelijk een lokale ontwikkelingsomgeving voor een Umbraco CMS-web-app maken met behulp van Visual Studio of WebMatrix.

- [Een Umbraco web-app maken met Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Een Umbraco web-app maken met WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Vergeet tooremove hello `install` map onder uw toepassing en upload nooit toostage of productie web-apps. Deze zelfstudie wordt WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Een testomgeving instellen
1. Maak een implementatiesleuf zoals eerder vermeld voor Hallo Umbraco CMS web-app, ervan uitgaande dat u hebt al een web-app Umbraco CMS up en wordt uitgevoerd. Als u dit niet doet, kunt u een van de Hallo Marketplace kunt maken.
2. Hallo-verbindingsreeks voor de fase implementatiesleuf toopoint toohello nieuwe bijwerken **umbraco-fase-db** database. Uw productie-web-app (umbraositecms-1) en het tijdelijke web-app (umbracositecms-1-fase) *moet* punt toodifferent databases.

    ![Bijwerken van de verbindingsreeks voor de web-app met nieuwe faseringsdatabase fasering](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Klik op **ophalen publicatie-instellingen** voor Hallo implementatiesleuf **fase**. Dit proces wordt een publiceren instellingenbestand downloaden dat alle Hallo informatie dat Visual Studio of WebMatrix toopublish uw toepassing hello lokale ontwikkeling web app toohello Azure-web-app moet wordt opgeslagen.

    ![Get-instelling van Hallo staging-web-app publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Open uw web-app voor lokale ontwikkeling in WebMatrix of Visual Studio. Deze zelfstudie wordt WebMatrix. U moet eerst tooimport Hallo publish settings-bestand voor uw tijdelijke web-app.

    ![Publicatie-instellingen voor Umbraco met behulp van Web Matrix importeren](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Controleer de wijzigingen in het dialoogvenster Hallo en uw lokale web app tooyour Azure-web-app implementeren *umbracositecms-1-fase*. Wanneer u bestanden rechtstreeks tooyour tijdelijke web-app implementeert, wordt u bestanden in Hallo weglaten `~/app_data/TEMP/` map omdat deze bestanden worden opnieuw gegenereerd wanneer het Hallo fase web-app eerst gestart. U moet ook Hallo weglaten `~/app_data/umbraco.config` bestand, dat ook worden opnieuw gegenereerd.

    ![Controleer de wijzigingen publiceren in web matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Nadat u Hallo Umbraco lokale web app toohello tijdelijke web-app is gepubliceerd, blader tooyour tijdelijke web-app en enkele tests toorule van problemen die worden uitgevoerd.

#### <a name="set-up-hello-courier2-deployment-module"></a>Hallo Courier2 implementatiemodule instellen
Hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) -module, u kunt gewoon met de rechtermuisknop op toopush inhoud, opmaakmodellen en modules van de ontwikkeling van een tijdelijke web-app tooa productie web-app. Dit proces vermindert Hallo risico's van uw web-app voor productie wanneer u een update implementeert op te splitsen.
Schaf een licentie voor Courier2 voor Hallo `*.azurewebsites.net` en uw aangepaste domein (bijvoorbeeld http://abc.com). Nadat u Hallo licentie koopt, plaats Hallo licentie gedownload (. LIC-bestand) in Hallo `bin` map.

![Licentiebestand onder de bin-map verwijderen](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Hallo Courier2 het downloadpakket](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Aanmelden tooyour fase web-app, stel http://umbracocms-site-stage.azurewebsites.net/umbraco, klikt u op Hallo **Developer** menu en klik vervolgens op **pakketten** > **installeren lokale pakket**.

    ![Het installatieprogramma Umbraco-pakket](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Hallo Courier2 pakket met Hallo installer uploaden.

    ![Pakket voor courier module uploaden](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. tooconfigure hello pakket, moet u tooupdate hello courier.config bestand onder Hallo **Config** map van uw web-app.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Onder `<repositories>`, Hallo productie site-URL en de gebruiker informatie invoeren.
    Als u van Hallo Umbraco standaardlidmaatschapsprovider gebruikmaakt, voegt u Hallo-ID voor Hallo beheer-gebruiker in Hallo &lt;gebruiker&gt; sectie.
    Als u een aangepaste Umbraco lidmaatschapsprovider, gebruikt u `<login>`,`<password>` op Hallo Courier2 module tooconnect toohello productiesite.
    Voor meer informatie [Hallo-documentatie voor Hallo Courier2 module lezen](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Op deze manier Hallo Courier2 module installeren op uw productiesite, en configureer deze toopoint toohello fase web-app in de respectieve courier.config bestand zoals hier wordt weergegeven.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Klik op Hallo **Courier2** hello Umbraco CMS web app dashboard tabblad en klik vervolgens op **locaties**. U ziet Hallo opslagplaats naam zoals vermeld in `courier.config`. Doe dit proces op uw productie- en staging-web-apps.

    ![Weergave bestemming web-app-opslagplaats](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. toodeploy inhoud van Hallo staging-site toohello productiesite en ga te**inhoud**, en selecteer een bestaande pagina of maak een nieuwe pagina. Ik selecteer een bestaande pagina Mijn web-app waarin Hallo titel van Hallo pagina is **aan de slag: nieuwe**, en klik vervolgens op **opslaan en publiceren**.

    ![Titel van pagina wijzigen en publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Klik met de rechtermuisknop Hallo gewijzigd pagina tooview alle Hallo-opties. Klik op **Courier** tooopen hello **implementatie** in het dialoogvenster. Klik op **implementeren** tooinitiate-implementatie.

    ![Dialoogvenster voor Courier module-implementatie](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Hallo-wijzigingen te controleren en klik vervolgens op **doorgaan**.

    ![Courier module implementatie dialoogvenster wijzigingen](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Hallo implementatielogboek toont als Hallo-implementatie geslaagd is.

     ![Logboeken van de implementatie van Courier module weergeven](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Blader uw productie-web-app toosee als Hallo wijzigingen worden doorgevoerd.

     ![Productie web-app bladeren](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

meer informatie over hoe toouse Courier, Raadpleeg de documentatie bij Hallo toolearn.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Hoe tooupgrade Hallo Umbraco CMS-versie
Courier wordt niet help u een upgrade van één versie van Umbraco CMS tooanother uitvoert. Wanneer u een Umbraco CMS-versie bijwerkt, moet u controleren op compatibiliteitsproblemen met uw aangepaste modules of modules van partners en Hallo Umbraco Core-bibliotheken. Hier vindt u aanbevolen procedures:

* Maak altijd een back-up van uw web-app en database voordat u een upgrade. U kunt op web-apps in Azure, automatische back-ups instellen voor uw websites met behulp van Hallo back-up en herstellen van uw site, indien nodig met behulp van de functie voor het terugzetten van Hallo. Zie voor meer informatie [hoe tooback van uw web-app](web-sites-backup.md) en [hoe toorestore uw web-app](web-sites-restore.md).
* Controleer of de pakketten van partners compatibel met Hallo-versie die u een uitvoert zijn naar upgrade. Pagina op Hallo-pakket te downloaden, controleert u Hallo project compatibiliteit met Umbraco CMS-versie.

Voor meer informatie over het tooupgrade uw web-app lokaal [Zie algemene upgraderichtlijnen hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Na de upgrade van uw lokale ontwikkeling-site publiceren Hallo wijzigingen toohello staging-web-app. Uw toepassing testen. Als alle er goed uitziet, gebruikt u Hallo **wisselen** knop tooswap uw staging site toohello productie web-app. Wanneer u Hallo gebruikt **wisselen** bewerking, kunt u Hallo-wijzigingen die worden beïnvloed weergeven in uw web-app-configuratie. Dit **wisselen** bewerking wisselt Hallo web-apps en -databases. Na het Hallo **wisselen**, web-app wordt punt toohello umbraco-fase-db productiedatabase Hallo en web-app wordt punt tooumbraco-prod-db faseringsdatabase Hallo.

![Voorbeeld voor het implementeren van Umbraco CMS wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Hier volgen voordelen van het wisselen van zowel Hallo WebApp en database Hallo:

* U kunt terugdraaien toohello eerdere versie van uw web-app met een andere **wisselen** als er toepassingsproblemen zijn.
* Voor een upgrade moet u toodeploy bestanden en databases van Hallo staging-web-app toohello productie web-app en database. Groot aantal dingen kunnen fout gaan wanneer u bestanden en databases implementeert. Met behulp van Hallo **wisselen** functie sleuven, we kunnen de uitvaltijd beperken tijdens een upgrade en Hallo risico's van fouten die zich voordoen kunnen bij het implementeren van wijzigingen te beperken.
* U kunt doen **A / B-tests** met behulp van Hallo [testen in productie](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) functie.

In dit voorbeeld ziet u de flexibiliteit van Hallo platform waar kunt u aangepaste modules vergelijkbare tooUmbraco Courier module toomanage implementatie in omgevingen Hallo.

## <a name="references"></a>Verwijzingen
[Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)

[Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)

[Hoe tooblock web toegang tot de implementatiesites toonon productie](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
