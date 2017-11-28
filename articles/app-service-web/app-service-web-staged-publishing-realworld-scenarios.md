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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="f2b51-103">DevOps-omgevingen effectief gebruiken voor uw web-apps</span><span class="sxs-lookup"><span data-stu-id="f2b51-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="f2b51-104">Dit artikel ziet u hoe tooset en beheren van implementaties van web application wanneer meerdere versies van uw toepassing zich in verschillende omgevingen zoals ontwikkeling, tijdelijke, kwaliteit assurance (QA) en productie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="f2b51-105">Elke versie van uw toepassing kan worden overwogen als een ontwikkelomgeving voor Hallo specifiek doel van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="f2b51-106">Ontwikkelaars kunnen bijvoorbeeld Hallo QA omgeving tootest Hallo kwaliteit van de toepassing hello gebruiken voordat ze Hallo wijzigingen tooproduction push.</span><span class="sxs-lookup"><span data-stu-id="f2b51-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="f2b51-107">Meerdere ontwikkelomgevingen kunnen worden een uitdaging omdat u nodig hebt tootrack code, middelen (berekening, web-app, database, cache, enzovoort) beheren en implementeren van code in omgevingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="f2b51-108">Instellen van een niet-productieomgeving (fase, Developer, QA)</span><span class="sxs-lookup"><span data-stu-id="f2b51-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="f2b51-109">Nadat een productie-web-app actief en werkend is, is de volgende stap Hallo toocreate een niet-productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f2b51-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="f2b51-110">toouse implementatiesites, zorg ervoor dat u in de modus voor Hallo Standard of Premium Azure App Service-abonnement worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="f2b51-111">Implementatiesites zijn live web-apps die hun eigen hostnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="f2b51-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="f2b51-112">Web-app inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van Hallo productiesite.</span><span class="sxs-lookup"><span data-stu-id="f2b51-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="f2b51-113">Wanneer u uw toepassing tooa-implementatiesleuf implementeert, kunt u krijgen Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f2b51-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="f2b51-114">U kunt wijzigingen tooa web-app in een gefaseerde installatie implementatiesleuf valideren voordat u Hallo-app met de productiesite Hallo wisselen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="f2b51-115">Wanneer u een web-appsite tooa eerst implementeren en deze in productie te wisselen, worden alle exemplaren van Hallo sleuf zich vóór gewisseld naar de productie opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="f2b51-116">Dit proces elimineert uitvaltijd wanneer u uw web-app implementeert.</span><span class="sxs-lookup"><span data-stu-id="f2b51-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="f2b51-117">Hallo verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd vanwege tooswap bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="f2b51-118">tooautomate deze volledige werkstroom configureren [automatisch wisselen](web-sites-staged-publishing.md#configure-auto-swap) wanneer vooraf swap-validatie is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="f2b51-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="f2b51-119">Als een wisseling heeft Hallo sleuf met Hallo eerder tijdelijke web-app nu Hallo vorige productie web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="f2b51-120">Als gewisseld naar de productiesite Hallo Hallo-wijzigingen zijn niet zoals u verwacht, kunt u Hallo uitvoeren dezelfde wisselen onmiddellijk tooget uw 'laatst bekende goede' web-app back.</span><span class="sxs-lookup"><span data-stu-id="f2b51-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="f2b51-121">Zie tooset van een gefaseerde installatie implementatiesleuf [faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f2b51-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="f2b51-122">Elke omgeving moet een eigen set resources bevatten.</span><span class="sxs-lookup"><span data-stu-id="f2b51-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="f2b51-123">Bijvoorbeeld, als uw web-app gebruikmaakt van een database, moeten klikt u vervolgens productie- en staging-web-apps gebruiken verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="f2b51-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="f2b51-124">Fasering development environment resources, zoals database-, opslag- of cache tooset uw ontwikkelomgeving staging toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="f2b51-125">Voorbeelden van het gebruik van meerdere ontwikkelomgevingen</span><span class="sxs-lookup"><span data-stu-id="f2b51-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="f2b51-126">Elk project beheer van gegevensbronnen code met ten minste twee omgevingen moet volgen: ontwikkeling en productie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="f2b51-127">Als u content management systems (CMSs), App-frameworks, enz., ondersteunen Hallo toepassing mogelijk niet in dit scenario zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="f2b51-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="f2b51-128">Dit deze is ingesteld op true voor een aantal Hallo populaire frameworks die worden besproken in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="f2b51-129">Groot aantal vragen horen toomind wanneer u met CMS/frameworks, zoals werkt:</span><span class="sxs-lookup"><span data-stu-id="f2b51-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="f2b51-130">Hoe u uitsplitsing Hallo inhoud in verschillende omgevingen?</span><span class="sxs-lookup"><span data-stu-id="f2b51-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="f2b51-131">Welke bestanden kunt u wijzigen zonder de framework-versie-updates</span><span class="sxs-lookup"><span data-stu-id="f2b51-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="f2b51-132">Hoe beheert u configuraties per omgeving?</span><span class="sxs-lookup"><span data-stu-id="f2b51-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="f2b51-133">Hoe beheert u versie-updates voor modules, invoegtoepassingen en Hallo basisschema?</span><span class="sxs-lookup"><span data-stu-id="f2b51-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="f2b51-134">Er zijn veel manieren tooset meerdere omgevingen voor uw project.</span><span class="sxs-lookup"><span data-stu-id="f2b51-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="f2b51-135">Hallo volgende voorbeelden ziet u een methode voor elke betreffende toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2b51-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="f2b51-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="f2b51-136">WordPress</span></span>
<span data-ttu-id="f2b51-137">In deze sectie leert u hoe tooset u een implementatiewerkstroom met behulp van WordPress sleuven.</span><span class="sxs-lookup"><span data-stu-id="f2b51-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="f2b51-138">WordPress, zoals de meeste CMS-oplossingen, ondersteunt geen meerdere ontwikkelomgevingen zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="f2b51-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="f2b51-139">functie voor Hallo-Web-Apps van Azure App Service heeft een aantal functies waarmee u eenvoudig toostore configuratie-instellingen buiten uw code.</span><span class="sxs-lookup"><span data-stu-id="f2b51-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="f2b51-140">Voordat u een faseringssleuf maken, instellen van uw toepassing code toosupport omgevingen met meerdere.</span><span class="sxs-lookup"><span data-stu-id="f2b51-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="f2b51-141">toosupport omgevingen met meerdere in WordPress, moet u tooedit `wp-config.php` op uw lokale ontwikkel web-app en het toevoegen van de volgende code aan begin van bestand Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="f2b51-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="f2b51-142">Dit proces wordt uw toepassing toopick Hallo juiste configuratie inschakelen op basis van geselecteerde Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2b51-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="f2b51-143">Maak een map onder de web-app root aangeroepen `config`, en voeg Hallo `wp-config.azure.php` en `wp-config.local.php` bestanden die uw Azure-omgeving en de lokale omgeving respectievelijk vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="f2b51-144">Kopieer de volgende Hallo in `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="f2b51-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="f2b51-145">Hallo-beveiligingssleutels instellen, zoals geïllustreerd in de vorige code Hallo kunt tooprevent uw web-app van gehackte wordt gebruik helpen, dus unieke waarden.</span><span class="sxs-lookup"><span data-stu-id="f2b51-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="f2b51-146">Als u toogenerate Hallo tekenreeks voor beveiligingssleutels vermeld in Hallo code nodig hebt, kunt u [Ga toohello automatische generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate nieuwe sleutel/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="f2b51-147">Kopiëren Hallo volgende code in `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="f2b51-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="f2b51-148">Relatieve paden gebruiken</span><span class="sxs-lookup"><span data-stu-id="f2b51-148">Use relative paths</span></span>
<span data-ttu-id="f2b51-149">Een laatste ding tooconfigure in Hallo WordPress-app is relatieve paden.</span><span class="sxs-lookup"><span data-stu-id="f2b51-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="f2b51-150">WordPress bevat gegevens van de URL in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f2b51-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="f2b51-151">Deze opslag is zwevend inhoud van de ene omgeving tooanother moeilijker.</span><span class="sxs-lookup"><span data-stu-id="f2b51-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="f2b51-152">Tooupdate hello database moet u elke keer dat u verplaatst van de lokale toostage of fase tooproduction omgevingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="f2b51-153">tooreduce hello risico van problemen die kunnen worden veroorzaakt bij de implementatie van een database telkens wanneer u vanaf de ene omgeving tooanother, gebruik Hallo implementeren [hoofdmap relatieve koppelingen invoegtoepassing](https://wordpress.org/plugins/root-relative-urls/), die u kunt installeren met behulp van Hallo WordPress-beheerder dashboard.</span><span class="sxs-lookup"><span data-stu-id="f2b51-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="f2b51-154">Hallo vermeldingen tooyour na toevoegen `wp-config.php` voordat Hallo `That's all, stop editing!` Opmerking:</span><span class="sxs-lookup"><span data-stu-id="f2b51-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="f2b51-155">Hallo-invoegtoepassing via Hallo activeren `Plugins` menu in het dashboard voor WordPress-beheerder.</span><span class="sxs-lookup"><span data-stu-id="f2b51-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="f2b51-156">Sla uw permalink-instellingen voor de WordPress-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="f2b51-157">Hallo laatste `wp-config.php` bestand</span><span class="sxs-lookup"><span data-stu-id="f2b51-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="f2b51-158">Eventuele updates van de core WordPress heeft geen invloed op uw `wp-config.php`, `wp-config.azure.php`, en `wp-config.local.php` bestanden.</span><span class="sxs-lookup"><span data-stu-id="f2b51-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="f2b51-159">Hier volgt een definitieve versie van Hallo `wp-config.php` bestand:</span><span class="sxs-lookup"><span data-stu-id="f2b51-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="f2b51-160">Een testomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f2b51-160">Set up a staging environment</span></span>
1. <span data-ttu-id="f2b51-161">Als u al een WordPress-web-app uitgevoerd op uw Azure-abonnement hebt, meld u aan toohello [Azure-portal](http://portal.azure.com), en ga tooyour WordPress-web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="f2b51-162">Als u een WordPress-web-app niet hebt, kunt u een van de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f2b51-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="f2b51-163">toolearn meer, Zie [een WordPress-web-app maken in Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="f2b51-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="f2b51-164">Klik op **instellingen** > **implementatiesites** > **toevoegen** toocreate een implementatiesleuf met de naam van de Hallo *fase*.</span><span class="sxs-lookup"><span data-stu-id="f2b51-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="f2b51-165">Een implementatiesleuf is een andere webtoepassing die shares Hallo dezelfde bronnen als Hallo primaire web-app die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f2b51-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Fase implementatiesleuf maken](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="f2b51-167">Toevoegen van een andere MySQL-database, spreek `wordpress-stage-db`, tooyour resourcegroep, `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="f2b51-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![MySQL-database tooresource groep toevoegen](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="f2b51-169">Hallo-verbindingstekenreeksen voor de fase implementatiesleuf toopoint toohello nieuwe database maken, bijwerken `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="f2b51-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="f2b51-170">Uw web-app van productie `wordpressprodapp`, en web-app voor fasering `wordpressprodapp-stage`, moet punt toodifferent databases.</span><span class="sxs-lookup"><span data-stu-id="f2b51-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="f2b51-171">Omgeving-specifieke app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="f2b51-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="f2b51-172">Ontwikkelaars kunnen sleutel-waardeparen tekenreeks opslaan in Azure als onderdeel van de configuratiegegevens hello, aangeroepen **Appinstellingen**, die is gekoppeld aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="f2b51-173">Tijdens runtime, web-apps automatisch deze waarden ophaalt en zodat ze beschikbaar toocode die in uw web-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="f2b51-174">Vanuit het beveiligingsoogpunt van die een voordeel nice aan clientzijde is omdat vertrouwelijke gegevens, zoals databaseverbindingsreeksen wachtwoorden, waaronder nooit worden weergegeven als leesbare tekst in een bestand, zoals `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="f2b51-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="f2b51-175">Dit proces wordt uitgelegd in Hallo na alinea's, is nuttig omdat het omvat zowel bestandswijzigingen en wijzigingen in de database voor Hallo WordPress-app:</span><span class="sxs-lookup"><span data-stu-id="f2b51-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="f2b51-176">Upgrade van de WordPress-versie</span><span class="sxs-lookup"><span data-stu-id="f2b51-176">WordPress version upgrade</span></span>
* <span data-ttu-id="f2b51-177">Nieuwe toevoegen of bewerken of upgraden van invoegtoepassingen</span><span class="sxs-lookup"><span data-stu-id="f2b51-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="f2b51-178">Nieuwe toevoegen of bewerken of upgraden van thema 's</span><span class="sxs-lookup"><span data-stu-id="f2b51-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="f2b51-179">Configureer appinstellingen voor:</span><span class="sxs-lookup"><span data-stu-id="f2b51-179">Configure app settings for:</span></span>

* <span data-ttu-id="f2b51-180">Database-informatie</span><span class="sxs-lookup"><span data-stu-id="f2b51-180">Database information</span></span>
* <span data-ttu-id="f2b51-181">In- en uitgeschakeld WordPress logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="f2b51-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="f2b51-182">WordPress-beveiligingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="f2b51-182">WordPress security settings</span></span>

![App-instellingen voor Wordpress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="f2b51-184">Zorg ervoor dat u de volgende app-instellingen voor uw web-app en fase productiesite Hallo toevoegt.</span><span class="sxs-lookup"><span data-stu-id="f2b51-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="f2b51-185">Houd er rekening mee dat Hallo productie web-app en fasering web-app verschillende databases gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f2b51-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="f2b51-186">Schakel Hallo **sleuf instelling** selectievakjes uit voor alle parameters van Hallo instellingen behalve WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="f2b51-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="f2b51-187">Dit proces wordt Hallo configuratie wisselen voor uw web-app, de inhoud van bestanden en de database.</span><span class="sxs-lookup"><span data-stu-id="f2b51-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="f2b51-188">Als **sleuf instelling** is dit selectievakje inschakelt, de app-instellingen en configuratie van de tekenreeks verbinding Hallo van web-app wordt *niet* verplaatsen tussen omgevingen bij het uitvoeren van een **wisselen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="f2b51-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="f2b51-189">Alle databasewijzigingen die aanwezig zijn, worden uw productie-web-app niet verbroken.</span><span class="sxs-lookup"><span data-stu-id="f2b51-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="f2b51-190">Hallo lokale ontwikkeling omgeving web app toohello fase web-app en database met WebMatrix of hulpprogramma's van uw keuze, zoals FTP, Git of PhpMyAdmin implementeren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Web Matrix publiceren dialoogvenster voor WordPress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="f2b51-192">Bladeren en test uw tijdelijke web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-192">Browse and test your staging web app.</span></span> <span data-ttu-id="f2b51-193">In overweging een scenario waarbij Hallo thema van web-app Hallo toobe bijgewerkt, moet u hier Hallo staging-web-app is.</span><span class="sxs-lookup"><span data-stu-id="f2b51-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Tijdelijke web-app bladeren voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="f2b51-195">Als alle er goed uitziet, klikt u op Hallo **wisselen** knop op uw tijdelijke web-app toomove uw inhoud toohello productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2b51-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="f2b51-196">In dit geval u Hallo WebApp en database Hallo wisselen tussen omgevingen tijdens elke **wisselen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="f2b51-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Voorbeeld van wijzigingen voor WordPress wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="f2b51-198">Als uw scenario moet tooonly push-bestanden (Er zijn geen updates van de database), moet u controleren **sleuf instelling** voor alle Hallo Databasegerelateerde *appinstellingen* en *verbinding tekenreeksen instellingen*in Hallo **Web-Appinstellingen** blade binnen hello Azure-portal voordat u Hallo **wisselen**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="f2b51-199">In dit geval DB_NAME, DB_HOST DB_PASSWORD, DB_USER en standaardinstellingen voor verbinding tekenreeks mag niet weergegeven in voorbeeld van wijzigingen Als u dit doet een **wisselen**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="f2b51-200">Op dit moment, wanneer u Hallo voltooid **wisselen** bewerking, wordt een WordPress-web-app hebt Hallo Hallo alleen bestanden worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f2b51-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="f2b51-201">Eerst een **wisselen**, hier is Hallo productie WordPress-web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="f2b51-202">![Web-app voor productie voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="f2b51-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="f2b51-203">Na het Hallo **wisselen** bewerking, Hallo thema is bijgewerkt op uw web-app voor productie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Web-app voor productie na sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="f2b51-205">Wanneer u tooroll weer nodig hebt, gaat u toohello productie web **Appinstellingen**, en klik op Hallo **wisselen** tooswap Hallo web-app en database uit productiesleuf toostaging knop.</span><span class="sxs-lookup"><span data-stu-id="f2b51-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="f2b51-206">Vergeet niet dat als wijzigingen in de database zijn opgenomen in een **wisselen** bewerking en vervolgens Hallo volgende keer dat u implementeert tooyour staging-web-app, moet u toodeploy Hallo database wijzigingen toohello huidige database voor uw tijdelijke web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="f2b51-207">de huidige database Hallo mogelijk Hallo vorige productie of Hallo fase van de database.</span><span class="sxs-lookup"><span data-stu-id="f2b51-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="f2b51-208">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f2b51-208">Summary</span></span>
<span data-ttu-id="f2b51-209">Hier volgt een algemene proces voor alle toepassingen die database heeft:</span><span class="sxs-lookup"><span data-stu-id="f2b51-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="f2b51-210">Hallo-toepassing installeren op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2b51-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="f2b51-211">Omgeving-specifieke configuraties (lokale en Azure Web Apps) bevatten.</span><span class="sxs-lookup"><span data-stu-id="f2b51-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="f2b51-212">Stel uw fasering en productie-omgevingen voor Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="f2b51-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="f2b51-213">Als u een productietoepassing die al wordt uitgevoerd op Azure hebt, synchroniseert u uw inhoud (bestanden/code en database) toolocal en fasering productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="f2b51-214">Uw toepassing ontwikkelen op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2b51-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="f2b51-215">Plaats uw productie-web-app of vergrendelde modus en inhoud van de database van toostaging en dev productieomgevingen synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="f2b51-216">Implementeer toohello staging-omgeving en testen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="f2b51-217">Tooproduction omgeving implementeren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="f2b51-218">Herhaal stap 4 tot en met 6.</span><span class="sxs-lookup"><span data-stu-id="f2b51-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="f2b51-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="f2b51-219">Umbraco</span></span>
<span data-ttu-id="f2b51-220">In deze sectie leert u hoe Hallo Umbraco CMS maakt gebruik van een aangepaste module toodeploy tussen meerdere DevOps-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="f2b51-221">In dit voorbeeld bevat een andere benadering toomanaging meerdere ontwikkelomgevingen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="f2b51-222">[Umbraco CMS](http://umbraco.com/) is een populair .NET CMS-oplossing die wordt gebruikt door veel ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="f2b51-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="f2b51-223">Het biedt Hallo [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy van ontwikkelomgevingen toostaging tooproduction.</span><span class="sxs-lookup"><span data-stu-id="f2b51-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="f2b51-224">U kunt gemakkelijk een lokale ontwikkelingsomgeving voor een Umbraco CMS-web-app maken met behulp van Visual Studio of WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f2b51-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="f2b51-225">Een Umbraco web-app maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2b51-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="f2b51-226">Een Umbraco web-app maken met WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f2b51-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="f2b51-227">Vergeet tooremove hello `install` map onder uw toepassing en upload nooit toostage of productie web-apps.</span><span class="sxs-lookup"><span data-stu-id="f2b51-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="f2b51-228">Deze zelfstudie wordt WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f2b51-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="f2b51-229">Een testomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f2b51-229">Set up a staging environment</span></span>
1. <span data-ttu-id="f2b51-230">Maak een implementatiesleuf zoals eerder vermeld voor Hallo Umbraco CMS web-app, ervan uitgaande dat u hebt al een web-app Umbraco CMS up en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="f2b51-231">Als u dit niet doet, kunt u een van de Hallo Marketplace kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f2b51-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="f2b51-232">Hallo-verbindingsreeks voor de fase implementatiesleuf toopoint toohello nieuwe bijwerken **umbraco-fase-db** database.</span><span class="sxs-lookup"><span data-stu-id="f2b51-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="f2b51-233">Uw productie-web-app (umbraositecms-1) en het tijdelijke web-app (umbracositecms-1-fase) *moet* punt toodifferent databases.</span><span class="sxs-lookup"><span data-stu-id="f2b51-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Bijwerken van de verbindingsreeks voor de web-app met nieuwe faseringsdatabase fasering](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="f2b51-235">Klik op **ophalen publicatie-instellingen** voor Hallo implementatiesleuf **fase**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="f2b51-236">Dit proces wordt een publiceren instellingenbestand downloaden dat alle Hallo informatie dat Visual Studio of WebMatrix toopublish uw toepassing hello lokale ontwikkeling web app toohello Azure-web-app moet wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Get-instelling van Hallo staging-web-app publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="f2b51-238">Open uw web-app voor lokale ontwikkeling in WebMatrix of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2b51-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="f2b51-239">Deze zelfstudie wordt WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f2b51-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="f2b51-240">U moet eerst tooimport Hallo publish settings-bestand voor uw tijdelijke web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Publicatie-instellingen voor Umbraco met behulp van Web Matrix importeren](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="f2b51-242">Controleer de wijzigingen in het dialoogvenster Hallo en uw lokale web app tooyour Azure-web-app implementeren *umbracositecms-1-fase*.</span><span class="sxs-lookup"><span data-stu-id="f2b51-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="f2b51-243">Wanneer u bestanden rechtstreeks tooyour tijdelijke web-app implementeert, wordt u bestanden in Hallo weglaten `~/app_data/TEMP/` map omdat deze bestanden worden opnieuw gegenereerd wanneer het Hallo fase web-app eerst gestart.</span><span class="sxs-lookup"><span data-stu-id="f2b51-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="f2b51-244">U moet ook Hallo weglaten `~/app_data/umbraco.config` bestand, dat ook worden opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Controleer de wijzigingen publiceren in web matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="f2b51-246">Nadat u Hallo Umbraco lokale web app toohello tijdelijke web-app is gepubliceerd, blader tooyour tijdelijke web-app en enkele tests toorule van problemen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="f2b51-247">Hallo Courier2 implementatiemodule instellen</span><span class="sxs-lookup"><span data-stu-id="f2b51-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="f2b51-248">Hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) -module, u kunt gewoon met de rechtermuisknop op toopush inhoud, opmaakmodellen en modules van de ontwikkeling van een tijdelijke web-app tooa productie web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="f2b51-249">Dit proces vermindert Hallo risico's van uw web-app voor productie wanneer u een update implementeert op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="f2b51-250">Schaf een licentie voor Courier2 voor Hallo `*.azurewebsites.net` en uw aangepaste domein (bijvoorbeeld http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="f2b51-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="f2b51-251">Nadat u Hallo licentie koopt, plaats Hallo licentie gedownload (. LIC-bestand) in Hallo `bin` map.</span><span class="sxs-lookup"><span data-stu-id="f2b51-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Licentiebestand onder de bin-map verwijderen](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="f2b51-253">[Hallo Courier2 het downloadpakket](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="f2b51-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="f2b51-254">Aanmelden tooyour fase web-app, stel http://umbracocms-site-stage.azurewebsites.net/umbraco, klikt u op Hallo **Developer** menu en klik vervolgens op **pakketten** > **installeren lokale pakket**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Het installatieprogramma Umbraco-pakket](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="f2b51-256">Hallo Courier2 pakket met Hallo installer uploaden.</span><span class="sxs-lookup"><span data-stu-id="f2b51-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Pakket voor courier module uploaden](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="f2b51-258">tooconfigure hello pakket, moet u tooupdate hello courier.config bestand onder Hallo **Config** map van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="f2b51-259">Onder `<repositories>`, Hallo productie site-URL en de gebruiker informatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="f2b51-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="f2b51-260">Als u van Hallo Umbraco standaardlidmaatschapsprovider gebruikmaakt, voegt u Hallo-ID voor Hallo beheer-gebruiker in Hallo &lt;gebruiker&gt; sectie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="f2b51-261">Als u een aangepaste Umbraco lidmaatschapsprovider, gebruikt u `<login>`,`<password>` op Hallo Courier2 module tooconnect toohello productiesite.</span><span class="sxs-lookup"><span data-stu-id="f2b51-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="f2b51-262">Voor meer informatie [Hallo-documentatie voor Hallo Courier2 module lezen](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="f2b51-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="f2b51-263">Op deze manier Hallo Courier2 module installeren op uw productiesite, en configureer deze toopoint toohello fase web-app in de respectieve courier.config bestand zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2b51-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="f2b51-264">Klik op Hallo **Courier2** hello Umbraco CMS web app dashboard tabblad en klik vervolgens op **locaties**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="f2b51-265">U ziet Hallo opslagplaats naam zoals vermeld in `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="f2b51-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="f2b51-266">Doe dit proces op uw productie- en staging-web-apps.</span><span class="sxs-lookup"><span data-stu-id="f2b51-266">Do this process on both your production and staging web apps.</span></span>

    ![Weergave bestemming web-app-opslagplaats](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="f2b51-268">toodeploy inhoud van Hallo staging-site toohello productiesite en ga te**inhoud**, en selecteer een bestaande pagina of maak een nieuwe pagina.</span><span class="sxs-lookup"><span data-stu-id="f2b51-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="f2b51-269">Ik selecteer een bestaande pagina Mijn web-app waarin Hallo titel van Hallo pagina is **aan de slag: nieuwe**, en klik vervolgens op **opslaan en publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Titel van pagina wijzigen en publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="f2b51-271">Klik met de rechtermuisknop Hallo gewijzigd pagina tooview alle Hallo-opties.</span><span class="sxs-lookup"><span data-stu-id="f2b51-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="f2b51-272">Klik op **Courier** tooopen hello **implementatie** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f2b51-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="f2b51-273">Klik op **implementeren** tooinitiate-implementatie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Dialoogvenster voor Courier module-implementatie](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="f2b51-275">Hallo-wijzigingen te controleren en klik vervolgens op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="f2b51-275">Review hello changes, and then click **Continue**.</span></span>

    ![Courier module implementatie dialoogvenster wijzigingen](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="f2b51-277">Hallo implementatielogboek toont als Hallo-implementatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="f2b51-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Logboeken van de implementatie van Courier module weergeven](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="f2b51-279">Blader uw productie-web-app toosee als Hallo wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2b51-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Productie web-app bladeren](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="f2b51-281">meer informatie over hoe toouse Courier, Raadpleeg de documentatie bij Hallo toolearn.</span><span class="sxs-lookup"><span data-stu-id="f2b51-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="f2b51-282">Hoe tooupgrade Hallo Umbraco CMS-versie</span><span class="sxs-lookup"><span data-stu-id="f2b51-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="f2b51-283">Courier wordt niet help u een upgrade van één versie van Umbraco CMS tooanother uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f2b51-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="f2b51-284">Wanneer u een Umbraco CMS-versie bijwerkt, moet u controleren op compatibiliteitsproblemen met uw aangepaste modules of modules van partners en Hallo Umbraco Core-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="f2b51-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="f2b51-285">Hier vindt u aanbevolen procedures:</span><span class="sxs-lookup"><span data-stu-id="f2b51-285">Here are best practices:</span></span>

* <span data-ttu-id="f2b51-286">Maak altijd een back-up van uw web-app en database voordat u een upgrade.</span><span class="sxs-lookup"><span data-stu-id="f2b51-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="f2b51-287">U kunt op web-apps in Azure, automatische back-ups instellen voor uw websites met behulp van Hallo back-up en herstellen van uw site, indien nodig met behulp van de functie voor het terugzetten van Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2b51-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="f2b51-288">Zie voor meer informatie [hoe tooback van uw web-app](web-sites-backup.md) en [hoe toorestore uw web-app](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f2b51-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="f2b51-289">Controleer of de pakketten van partners compatibel met Hallo-versie die u een uitvoert zijn naar upgrade.</span><span class="sxs-lookup"><span data-stu-id="f2b51-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="f2b51-290">Pagina op Hallo-pakket te downloaden, controleert u Hallo project compatibiliteit met Umbraco CMS-versie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="f2b51-291">Voor meer informatie over het tooupgrade uw web-app lokaal [Zie algemene upgraderichtlijnen hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="f2b51-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="f2b51-292">Na de upgrade van uw lokale ontwikkeling-site publiceren Hallo wijzigingen toohello staging-web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="f2b51-293">Uw toepassing testen.</span><span class="sxs-lookup"><span data-stu-id="f2b51-293">Test your application.</span></span> <span data-ttu-id="f2b51-294">Als alle er goed uitziet, gebruikt u Hallo **wisselen** knop tooswap uw staging site toohello productie web-app.</span><span class="sxs-lookup"><span data-stu-id="f2b51-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="f2b51-295">Wanneer u Hallo gebruikt **wisselen** bewerking, kunt u Hallo-wijzigingen die worden beïnvloed weergeven in uw web-app-configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="f2b51-296">Dit **wisselen** bewerking wisselt Hallo web-apps en -databases.</span><span class="sxs-lookup"><span data-stu-id="f2b51-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="f2b51-297">Na het Hallo **wisselen**, web-app wordt punt toohello umbraco-fase-db productiedatabase Hallo en web-app wordt punt tooumbraco-prod-db faseringsdatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2b51-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Voorbeeld voor het implementeren van Umbraco CMS wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="f2b51-299">Hier volgen voordelen van het wisselen van zowel Hallo WebApp en database Hallo:</span><span class="sxs-lookup"><span data-stu-id="f2b51-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="f2b51-300">U kunt terugdraaien toohello eerdere versie van uw web-app met een andere **wisselen** als er toepassingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="f2b51-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="f2b51-301">Voor een upgrade moet u toodeploy bestanden en databases van Hallo staging-web-app toohello productie web-app en database.</span><span class="sxs-lookup"><span data-stu-id="f2b51-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="f2b51-302">Groot aantal dingen kunnen fout gaan wanneer u bestanden en databases implementeert.</span><span class="sxs-lookup"><span data-stu-id="f2b51-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="f2b51-303">Met behulp van Hallo **wisselen** functie sleuven, we kunnen de uitvaltijd beperken tijdens een upgrade en Hallo risico's van fouten die zich voordoen kunnen bij het implementeren van wijzigingen te beperken.</span><span class="sxs-lookup"><span data-stu-id="f2b51-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="f2b51-304">U kunt doen **A / B-tests** met behulp van Hallo [testen in productie](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) functie.</span><span class="sxs-lookup"><span data-stu-id="f2b51-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="f2b51-305">In dit voorbeeld ziet u de flexibiliteit van Hallo platform waar kunt u aangepaste modules vergelijkbare tooUmbraco Courier module toomanage implementatie in omgevingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2b51-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="f2b51-306">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="f2b51-306">References</span></span>
[<span data-ttu-id="f2b51-307">Flexibele software ontwikkelen met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f2b51-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="f2b51-308">Faseringsomgevingen voor web-apps in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="f2b51-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="f2b51-309">Hoe tooblock web toegang tot de implementatiesites toonon productie</span><span class="sxs-lookup"><span data-stu-id="f2b51-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
