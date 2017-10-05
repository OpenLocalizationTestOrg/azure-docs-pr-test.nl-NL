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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="c2720-103">DevOps-omgevingen effectief gebruiken voor uw web-apps</span><span class="sxs-lookup"><span data-stu-id="c2720-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="c2720-104">In dit artikel laat zien hoe instellen en beheren van implementaties van web application wanneer meerdere versies van uw toepassing zich in verschillende omgevingen zoals ontwikkeling, tijdelijke, kwaliteit assurance (QA) en productie.</span><span class="sxs-lookup"><span data-stu-id="c2720-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="c2720-105">Elke versie van uw toepassing kan worden overwogen als een ontwikkelomgeving voor het specifieke doel van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="c2720-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="c2720-106">Ontwikkelaars kunnen bijvoorbeeld de QA-omgeving gebruiken voor het testen van de kwaliteit van de toepassing voordat ze push de wijzigingen naar productie.</span><span class="sxs-lookup"><span data-stu-id="c2720-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="c2720-107">Meerdere ontwikkelomgevingen kunnen een uitdaging zijn, omdat u wilt bijhouden code, middelen (berekening, web-app, database, cache, enzovoort) beheren en code implementeren in omgevingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="c2720-108">Instellen van een niet-productieomgeving (fase, Developer, QA)</span><span class="sxs-lookup"><span data-stu-id="c2720-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="c2720-109">Nadat een productie-web-app actief en werkend is, wordt de volgende stap is het maken van een niet-productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c2720-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="c2720-110">Zorg dat u in de Standard of Premium Azure App Service plan-modus worden uitgevoerd voor het gebruik van implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="c2720-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="c2720-111">Implementatiesites zijn live web-apps die hun eigen hostnamen hebben.</span><span class="sxs-lookup"><span data-stu-id="c2720-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="c2720-112">Web-app inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van de productiesite.</span><span class="sxs-lookup"><span data-stu-id="c2720-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="c2720-113">Als u uw toepassing op een implementatiesleuf implementeert, krijgt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c2720-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="c2720-114">U kunt wijzigingen in een web-app in een gefaseerde installatie implementatiesleuf valideren voordat het wisselen van de app met de productiesite.</span><span class="sxs-lookup"><span data-stu-id="c2720-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="c2720-115">Wanneer u een WebApp in een sleuf eerst implementeren en deze in productie te wisselen, worden alle exemplaren van de sleuf zich vóór gewisseld naar de productie opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="c2720-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="c2720-116">Dit proces elimineert uitvaltijd wanneer u uw web-app implementeert.</span><span class="sxs-lookup"><span data-stu-id="c2720-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="c2720-117">Het verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd omdat swap-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="c2720-118">Configureren voor het automatiseren van deze volledige werkstroom [automatisch wisselen](web-sites-staged-publishing.md#configure-auto-swap) wanneer vooraf swap-validatie is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="c2720-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="c2720-119">Als een wisseling heeft de sleuf waarin de eerder voorbereide web-app nu is de vorige productie web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="c2720-120">Als de gewisseld naar de productiesite wijzigingen zijn niet zoals u verwacht, kunt u de dezelfde swap uitvoeren onmiddellijk om uw web-'laatste bekende juiste configuratie' back-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="c2720-121">Als u een gefaseerde installatie implementatiesleuf instelt, Zie [faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c2720-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="c2720-122">Elke omgeving moet een eigen set resources bevatten.</span><span class="sxs-lookup"><span data-stu-id="c2720-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="c2720-123">Bijvoorbeeld, als uw web-app gebruikmaakt van een database, moeten klikt u vervolgens productie- en staging-web-apps gebruiken verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="c2720-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="c2720-124">Fasering ontwikkeling omgeving resources zoals database-, opslag- of -cache in te stellen uw ontwikkelomgeving staging toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c2720-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="c2720-125">Voorbeelden van het gebruik van meerdere ontwikkelomgevingen</span><span class="sxs-lookup"><span data-stu-id="c2720-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="c2720-126">Elk project beheer van gegevensbronnen code met ten minste twee omgevingen moet volgen: ontwikkeling en productie.</span><span class="sxs-lookup"><span data-stu-id="c2720-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="c2720-127">Als u content management systems (CMSs), App-frameworks, enz., ondersteunen de toepassing mogelijk niet in dit scenario zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="c2720-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="c2720-128">Dit deze is ingesteld op true voor een aantal van de gebruikte frameworks die in de volgende secties worden besproken.</span><span class="sxs-lookup"><span data-stu-id="c2720-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="c2720-129">Groot aantal vragen keert naar rekening wanneer u met CMS/frameworks, zoals werkt:</span><span class="sxs-lookup"><span data-stu-id="c2720-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="c2720-130">Hoe u de inhoud uit opdelen in verschillende omgevingen?</span><span class="sxs-lookup"><span data-stu-id="c2720-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="c2720-131">Welke bestanden kunt u wijzigen zonder de framework-versie-updates</span><span class="sxs-lookup"><span data-stu-id="c2720-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="c2720-132">Hoe beheert u configuraties per omgeving?</span><span class="sxs-lookup"><span data-stu-id="c2720-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="c2720-133">Hoe beheert u versie-updates voor modules, invoegtoepassingen en het framework core?</span><span class="sxs-lookup"><span data-stu-id="c2720-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="c2720-134">Er zijn veel manieren voor het instellen van meerdere omgevingen voor uw project.</span><span class="sxs-lookup"><span data-stu-id="c2720-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="c2720-135">De volgende voorbeelden ziet een methode voor elke betreffende toepassing.</span><span class="sxs-lookup"><span data-stu-id="c2720-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="c2720-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="c2720-136">WordPress</span></span>
<span data-ttu-id="c2720-137">In deze sectie leert u hoe u een werkstroom voor de implementatie met behulp van sleuven voor WordPress instelt.</span><span class="sxs-lookup"><span data-stu-id="c2720-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="c2720-138">WordPress, zoals de meeste CMS-oplossingen, ondersteunt geen meerdere ontwikkelomgevingen zonder aanpassing.</span><span class="sxs-lookup"><span data-stu-id="c2720-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="c2720-139">De functie Web Apps van Azure App Service heeft enkele functies om gemakkelijk voor het opslaan van configuratie-instellingen buiten uw code.</span><span class="sxs-lookup"><span data-stu-id="c2720-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="c2720-140">Voordat u een faseringssleuf maakt, kunt u instellen van uw toepassingscode ter ondersteuning van meerdere omgevingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="c2720-141">Ter ondersteuning van meerdere omgevingen in WordPress, moet u bewerken `wp-config.php` op uw lokale ontwikkel web-app en voeg de volgende code toe aan het begin van het bestand.</span><span class="sxs-lookup"><span data-stu-id="c2720-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="c2720-142">Dit proces wordt uw toepassing om op te halen van de juiste configuratie op basis van de geselecteerde omgeving inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c2720-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

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

2. <span data-ttu-id="c2720-143">Maak een map onder de web-app root aangeroepen `config`, en voeg de `wp-config.azure.php` en `wp-config.local.php` bestanden die uw Azure-omgeving en de lokale omgeving respectievelijk vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="c2720-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="c2720-144">Kopieer de volgende in `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="c2720-144">Copy the following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="c2720-145">Instellen van de beveiliging sleutels zoals geïllustreerd in de vorige code helpen kunnen om te voorkomen dat uw web-app wordt gehackte unieke waarden dus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c2720-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="c2720-146">Als u nodig hebt voor het genereren van de tekenreeks voor beveiligingssleutels vermeld in de code, kunt u [gaat u naar de automatische generator](https://api.wordpress.org/secret-key/1.1/salt) voor het maken van nieuwe sleutel/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="c2720-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="c2720-147">Kopieer de volgende code in `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="c2720-147">Copy the following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="c2720-148">Relatieve paden gebruiken</span><span class="sxs-lookup"><span data-stu-id="c2720-148">Use relative paths</span></span>
<span data-ttu-id="c2720-149">Een ding te configureren in de WordPress-app is relatieve paden.</span><span class="sxs-lookup"><span data-stu-id="c2720-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="c2720-150">WordPress bevat gegevens van de URL in de database.</span><span class="sxs-lookup"><span data-stu-id="c2720-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="c2720-151">Deze opslag maakt verplaatsen inhoud van de ene omgeving naar een andere moeilijker.</span><span class="sxs-lookup"><span data-stu-id="c2720-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="c2720-152">U moet de database bijwerken telkens wanneer u van lokale naar werkgebied of fase naar productieomgevingen verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c2720-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="c2720-153">Om het risico van problemen die kunnen worden veroorzaakt bij de implementatie van een database telkens wanneer u van de ene omgeving naar een andere implementeren, gebruiken de [hoofdmap relatieve koppelingen invoegtoepassing](https://wordpress.org/plugins/root-relative-urls/), die u kunt installeren met behulp van het dashboard WordPress-beheerder.</span><span class="sxs-lookup"><span data-stu-id="c2720-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="c2720-154">De volgende items aan uw `wp-config.php` bestand voordat de `That's all, stop editing!` Opmerking:</span><span class="sxs-lookup"><span data-stu-id="c2720-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="c2720-155">Activeren van de invoegtoepassing via het `Plugins` menu in het dashboard voor WordPress-beheerder.</span><span class="sxs-lookup"><span data-stu-id="c2720-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="c2720-156">Sla uw permalink-instellingen voor de WordPress-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="c2720-157">De laatste `wp-config.php` bestand</span><span class="sxs-lookup"><span data-stu-id="c2720-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="c2720-158">Eventuele updates van de core WordPress heeft geen invloed op uw `wp-config.php`, `wp-config.azure.php`, en `wp-config.local.php` bestanden.</span><span class="sxs-lookup"><span data-stu-id="c2720-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="c2720-159">Hier volgt een definitieve versie van de `wp-config.php` bestand:</span><span class="sxs-lookup"><span data-stu-id="c2720-159">Here's a final version of the `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="c2720-160">Een testomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="c2720-160">Set up a staging environment</span></span>
1. <span data-ttu-id="c2720-161">Als u al een WordPress-web-app uitgevoerd op uw Azure-abonnement hebt, meld u bij de [Azure-portal](http://portal.azure.com), en gaat u naar uw WordPress-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="c2720-162">Als u een WordPress-web-app niet hebt, kunt u een vanuit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c2720-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="c2720-163">Zie voor meer informatie, [een WordPress-web-app maken in Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="c2720-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="c2720-164">Klik op **instellingen** > **implementatiesites** > **toevoegen** een implementatiesleuf te maken met de naam *fase* .</span><span class="sxs-lookup"><span data-stu-id="c2720-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="c2720-165">Een implementatiesleuf is een andere webtoepassing die dezelfde bronnen als de primaire web-app die u eerder hebt gemaakt, deelt.</span><span class="sxs-lookup"><span data-stu-id="c2720-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Fase implementatiesleuf maken](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="c2720-167">Toevoegen van een andere MySQL-database, spreek `wordpress-stage-db`, aan de resourcegroep `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="c2720-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![MySQL-database toevoegen aan resourcegroep](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="c2720-169">Werk de verbindingsreeksen voor uw implementatiesleuf fase verwijzen naar de nieuwe database `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="c2720-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="c2720-170">Uw web-app van productie `wordpressprodapp`, en web-app voor fasering `wordpressprodapp-stage`, moet verwijzen naar andere databases.</span><span class="sxs-lookup"><span data-stu-id="c2720-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="c2720-171">Omgeving-specifieke app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="c2720-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="c2720-172">Ontwikkelaars kunnen sleutel-waardeparen tekenreeks opslaan in Azure als onderdeel van de configuratie-informatie, aangeroepen **Appinstellingen**, die is gekoppeld aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="c2720-173">Tijdens runtime, web-apps automatisch deze waarden ophaalt en beschikbaar stellen aan code die wordt uitgevoerd in uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="c2720-174">Vanuit het beveiligingsoogpunt van die een voordeel nice aan clientzijde is omdat vertrouwelijke gegevens, zoals databaseverbindingsreeksen wachtwoorden, waaronder nooit worden weergegeven als leesbare tekst in een bestand, zoals `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="c2720-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="c2720-175">Dit proces wordt uitgelegd in de volgende leden, is nuttig omdat het omvat zowel bestandswijzigingen en wijzigingen in de database voor de WordPress-app:</span><span class="sxs-lookup"><span data-stu-id="c2720-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="c2720-176">Upgrade van de WordPress-versie</span><span class="sxs-lookup"><span data-stu-id="c2720-176">WordPress version upgrade</span></span>
* <span data-ttu-id="c2720-177">Nieuwe toevoegen of bewerken of upgraden van invoegtoepassingen</span><span class="sxs-lookup"><span data-stu-id="c2720-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="c2720-178">Nieuwe toevoegen of bewerken of upgraden van thema 's</span><span class="sxs-lookup"><span data-stu-id="c2720-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="c2720-179">Configureer appinstellingen voor:</span><span class="sxs-lookup"><span data-stu-id="c2720-179">Configure app settings for:</span></span>

* <span data-ttu-id="c2720-180">Database-informatie</span><span class="sxs-lookup"><span data-stu-id="c2720-180">Database information</span></span>
* <span data-ttu-id="c2720-181">In- en uitgeschakeld WordPress logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="c2720-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="c2720-182">WordPress-beveiligingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="c2720-182">WordPress security settings</span></span>

![App-instellingen voor Wordpress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="c2720-184">Zorg ervoor dat u de volgende appinstellingen voor uw web-app en fase productiesite toevoegt.</span><span class="sxs-lookup"><span data-stu-id="c2720-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="c2720-185">Houd er rekening mee dat de web-app voor productie en fasering web-app gebruikmaken van verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="c2720-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="c2720-186">Schakel de **sleuf instelling** selectievakjes uit voor alle instellingen-parameters behalve WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="c2720-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="c2720-187">Dit proces wordt wisselen van de configuratie voor uw web-app, de inhoud van bestanden en de database.</span><span class="sxs-lookup"><span data-stu-id="c2720-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="c2720-188">Als **sleuf instelling** is ingeschakeld, de app-instellingen en de verbinding van de web-app string configuratie wordt *niet* verplaatsen tussen omgevingen bij het uitvoeren van een **wisselen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="c2720-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="c2720-189">Alle databasewijzigingen die aanwezig zijn, worden uw productie-web-app niet verbroken.</span><span class="sxs-lookup"><span data-stu-id="c2720-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="c2720-190">De ontwikkeling van lokale omgeving web-app implementeren op de fase web-app en de database met WebMatrix of hulpprogramma's van uw keuze, zoals FTP, Git of PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="c2720-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Web Matrix publiceren dialoogvenster voor WordPress-web-app](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="c2720-192">Bladeren en test uw tijdelijke web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-192">Browse and test your staging web app.</span></span> <span data-ttu-id="c2720-193">In overweging een scenario waarbij het thema van de web-app worden bijgewerkt, is dit de tijdelijke web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Tijdelijke web-app bladeren voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="c2720-195">Als alle er goed uitziet, klikt u op de **wisselen** knop op uw web-app Test uw inhoud verplaatsen naar de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c2720-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="c2720-196">In dit geval u de web-app en de database wisselen tussen omgevingen tijdens elke **wisselen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="c2720-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Voorbeeld van wijzigingen voor WordPress wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="c2720-198">Als uw scenario moet alleen push-bestanden (Er zijn geen updates van de database), moet u controleren **sleuf instelling** voor alle de database-gerelateerde *appinstellingen* en *verbinding tekenreeksen instellingen* in de **Web-Appinstellingen** blade binnen de Azure-portal eerst de **wisselen**.</span><span class="sxs-lookup"><span data-stu-id="c2720-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="c2720-199">In dit geval DB_NAME, DB_HOST DB_PASSWORD, DB_USER en standaardinstellingen voor verbinding tekenreeks mag niet weergegeven in voorbeeld van wijzigingen Als u dit doet een **wisselen**.</span><span class="sxs-lookup"><span data-stu-id="c2720-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="c2720-200">Op dit moment kunt u wanneer de **wisselen** bewerking, de WordPress-web-app heeft alleen de updatebestanden.</span><span class="sxs-lookup"><span data-stu-id="c2720-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="c2720-201">Eerst een **wisselen**, hier is de productie WordPress-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="c2720-202">![Web-app voor productie voordat sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="c2720-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="c2720-203">Na de **wisselen** bewerking, het thema is bijgewerkt op uw web-app voor productie.</span><span class="sxs-lookup"><span data-stu-id="c2720-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Web-app voor productie na sleuven wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="c2720-205">Als u terugdraaien wilt, gaat u naar het web productie **App-instellingen**, en klik op de **wisselen** knop wisselen van de web-app en de database van de productie te faseringssleuf gewisseld.</span><span class="sxs-lookup"><span data-stu-id="c2720-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="c2720-206">Vergeet niet dat als wijzigingen in de database zijn opgenomen in een **wisselen** bewerking, klikt u vervolgens de volgende keer dat u voor uw tijdelijke web-app implementeert, moet u wijzigingen in de database voor de huidige database voor uw tijdelijke web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="c2720-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="c2720-207">De huidige database is mogelijk de vorige productiedatabase of de fase-database.</span><span class="sxs-lookup"><span data-stu-id="c2720-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="c2720-208">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c2720-208">Summary</span></span>
<span data-ttu-id="c2720-209">Hier volgt een algemene proces voor alle toepassingen die database heeft:</span><span class="sxs-lookup"><span data-stu-id="c2720-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="c2720-210">Installeer de toepassing op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="c2720-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="c2720-211">Omgeving-specifieke configuraties (lokale en Azure Web Apps) bevatten.</span><span class="sxs-lookup"><span data-stu-id="c2720-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="c2720-212">Stel uw fasering en productie-omgevingen voor Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="c2720-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="c2720-213">Als u een productietoepassing die al wordt uitgevoerd op Azure hebt, synchroniseert uw productie-inhoud (bestanden/code en database) naar de lokale en staging-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="c2720-214">Uw toepassing ontwikkelen op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="c2720-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="c2720-215">Plaats uw productie-web-app of vergrendelde modus en inhoud van de database van de productie naar faserings- en Developer-omgevingen te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="c2720-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="c2720-216">Implementeer aan de staging-omgeving en de test.</span><span class="sxs-lookup"><span data-stu-id="c2720-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="c2720-217">Implementeren naar productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c2720-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="c2720-218">Herhaal stap 4 tot en met 6.</span><span class="sxs-lookup"><span data-stu-id="c2720-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="c2720-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="c2720-219">Umbraco</span></span>
<span data-ttu-id="c2720-220">In deze sectie leert u hoe de Umbraco CMS een aangepaste module gebruikt om te implementeren in omgevingen met meerdere DevOps.</span><span class="sxs-lookup"><span data-stu-id="c2720-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="c2720-221">In dit voorbeeld bevat een andere benadering voor het beheren van meerdere ontwikkelomgevingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="c2720-222">[Umbraco CMS](http://umbraco.com/) is een populair .NET CMS-oplossing die wordt gebruikt door veel ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="c2720-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="c2720-223">Biedt de [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module voor het implementeren van ontwikkeling voor fasering naar productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="c2720-224">U kunt gemakkelijk een lokale ontwikkelingsomgeving voor een Umbraco CMS-web-app maken met behulp van Visual Studio of WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c2720-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="c2720-225">Een Umbraco web-app maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2720-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="c2720-226">Een Umbraco web-app maken met WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c2720-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="c2720-227">Vergeet verwijderen van de `install` map onder uw toepassing en nooit naar werkgebied of productie web-apps te uploaden.</span><span class="sxs-lookup"><span data-stu-id="c2720-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="c2720-228">Deze zelfstudie wordt WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c2720-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="c2720-229">Een testomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="c2720-229">Set up a staging environment</span></span>
1. <span data-ttu-id="c2720-230">Maak een implementatiesleuf zoals eerder vermeld voor de webtoepassing Umbraco CMS, ervan uitgaande dat u hebt al een web-app Umbraco CMS up en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2720-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="c2720-231">Als u dit niet doet, kunt u een van de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c2720-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="c2720-232">Bijwerken van de verbindingsreeks voor de implementatiesleuf fase verwijzen naar de nieuwe **umbraco-fase-db** database.</span><span class="sxs-lookup"><span data-stu-id="c2720-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="c2720-233">Uw productie-web-app (umbraositecms-1) en het tijdelijke web-app (umbracositecms-1-fase) *moet* verwijzen naar andere databases.</span><span class="sxs-lookup"><span data-stu-id="c2720-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Bijwerken van de verbindingsreeks voor de web-app met nieuwe faseringsdatabase fasering](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="c2720-235">Klik op **ophalen publicatie-instellingen** voor de implementatiesleuf **fase**.</span><span class="sxs-lookup"><span data-stu-id="c2720-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="c2720-236">Dit proces zal een instellingenbestand publiceren met de gegevens die Visual Studio of WebMatrix nodig heeft om uw toepassing publiceren vanuit de lokale ontwikkeling web-app in de Azure-web-app downloaden.</span><span class="sxs-lookup"><span data-stu-id="c2720-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Get-instelling van de tijdelijke web-app publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="c2720-238">Open uw web-app voor lokale ontwikkeling in WebMatrix of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2720-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="c2720-239">Deze zelfstudie wordt WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="c2720-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="c2720-240">U moet eerst de publish settings-bestand voor uw tijdelijke web-app importeren.</span><span class="sxs-lookup"><span data-stu-id="c2720-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Publicatie-instellingen voor Umbraco met behulp van Web Matrix importeren](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="c2720-242">Controleer de wijzigingen in het dialoogvenster en uw lokale web-app implementeren in uw Azure-web-app *umbracositecms-1-fase*.</span><span class="sxs-lookup"><span data-stu-id="c2720-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="c2720-243">Wanneer u bestanden rechtstreeks naar uw tijdelijke web-app implementeert, wordt u weglaten bestanden in de `~/app_data/TEMP/` map omdat deze bestanden worden opnieuw gegenereerd wanneer de fase web-app eerst gestart.</span><span class="sxs-lookup"><span data-stu-id="c2720-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="c2720-244">U moet ook weglaten de `~/app_data/umbraco.config` -bestand, dat ook worden opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c2720-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Controleer de wijzigingen publiceren in web matrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="c2720-246">Nadat u de Umbraco lokale web-app is gepubliceerd naar de tijdelijke web-app, blader naar uw tijdelijke web-app en enkele tests sprake is van eventuele problemen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c2720-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="c2720-247">De module Courier2 implementatie instellen</span><span class="sxs-lookup"><span data-stu-id="c2720-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="c2720-248">Met de [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, u kunt gewoon met de rechtermuisknop op push-inhoud, opmaakmodellen en modules voor ontwikkeling van een tijdelijke web-app in een productie-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="c2720-249">Dit proces vermindert het risico van uw web-app voor productie wanneer u een update implementeert op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="c2720-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="c2720-250">Schaf een licentie voor Courier2 voor de `*.azurewebsites.net` en uw aangepaste domein (bijvoorbeeld http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="c2720-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="c2720-251">Nadat u de licentie koopt, plaatst u de gedownloade licentie (. LIC-bestand) in de `bin` map.</span><span class="sxs-lookup"><span data-stu-id="c2720-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Licentiebestand onder de bin-map verwijderen](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="c2720-253">[Download het pakket Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="c2720-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="c2720-254">Aanmelden bij uw fase web-app spreek http://umbracocms-site-stage.azurewebsites.net/umbraco, klikt u op de **Developer** menu en klik vervolgens op **pakketten** > **lokaal installeren pakket**.</span><span class="sxs-lookup"><span data-stu-id="c2720-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Het installatieprogramma Umbraco-pakket](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="c2720-256">Upload het pakket Courier2 met behulp van het installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="c2720-256">Upload the Courier2 package by using the installer.</span></span>

    ![Pakket voor courier module uploaden](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="c2720-258">Voor het configureren van het pakket dat u wilt bijwerken van het bestand courier.config onder de **Config** map van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="c2720-259">Onder `<repositories>`, geef de URL en de gebruiker-informatie voor de site voor productie.</span><span class="sxs-lookup"><span data-stu-id="c2720-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="c2720-260">Als u de standaardprovider Umbraco-lidmaatschap gebruikt, voegt u de ID voor de beheer-gebruiker in de &lt;gebruiker&gt; sectie.</span><span class="sxs-lookup"><span data-stu-id="c2720-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="c2720-261">Als u een aangepaste Umbraco lidmaatschapsprovider, gebruikt u `<login>`,`<password>` in de module Courier2 verbinding maken met de productiesite.</span><span class="sxs-lookup"><span data-stu-id="c2720-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="c2720-262">Voor meer informatie [Raadpleeg de documentatie voor de module Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="c2720-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="c2720-263">Op dezelfde manier de Courier2-module installeren op uw productiesite, en configureer deze om te verwijzen naar de web-app voor de fase in het bestand van de respectieve courier.config zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c2720-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="c2720-264">Klik op de **Courier2** tabblad in het dashboard Umbraco CMS web app en klik vervolgens op **locaties**.</span><span class="sxs-lookup"><span data-stu-id="c2720-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="c2720-265">U ziet de naam van de opslagplaats op zoals vermeld in `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="c2720-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="c2720-266">Doe dit proces op uw productie- en staging-web-apps.</span><span class="sxs-lookup"><span data-stu-id="c2720-266">Do this process on both your production and staging web apps.</span></span>

    ![Weergave bestemming web-app-opslagplaats](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="c2720-268">Ga voor het implementeren van inhoud van de staging-site naar de productiesite naar **inhoud**, en selecteer een bestaande pagina of maak een nieuwe pagina.</span><span class="sxs-lookup"><span data-stu-id="c2720-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="c2720-269">Ik selecteer een bestaande pagina Mijn web-app waarin de titel van de pagina is **aan de slag: nieuwe**, en klik vervolgens op **opslaan en publiceren**.</span><span class="sxs-lookup"><span data-stu-id="c2720-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Titel van pagina wijzigen en publiceren](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="c2720-271">Met de rechtermuisknop op de gewijzigde pagina om alle opties weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c2720-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="c2720-272">Klik op **Courier** openen de **implementatie** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c2720-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="c2720-273">Klik op **implementeren** implementatie te starten.</span><span class="sxs-lookup"><span data-stu-id="c2720-273">Click **Deploy** to initiate deployment.</span></span>

    ![Dialoogvenster voor Courier module-implementatie](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="c2720-275">Controleer de wijzigingen en klik vervolgens op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="c2720-275">Review the changes, and then click **Continue**.</span></span>

    ![Courier module implementatie dialoogvenster wijzigingen](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="c2720-277">Het implementatielogboek bevat als de implementatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="c2720-277">The deployment log shows if the deployment was successful.</span></span>

     ![Logboeken van de implementatie van Courier module weergeven](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="c2720-279">Blader uw productie-web-app om te zien als de wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2720-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Productie web-app bladeren](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="c2720-281">Raadpleeg de documentatie voor meer informatie over het gebruik van Courier.</span><span class="sxs-lookup"><span data-stu-id="c2720-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="c2720-282">Het bijwerken van de Umbraco CMS-versie</span><span class="sxs-lookup"><span data-stu-id="c2720-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="c2720-283">Courier wordt niet help u een upgrade van één versie van Umbraco CMS naar een andere uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c2720-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="c2720-284">Wanneer u een Umbraco CMS-versie bijwerkt, moet u controleren voor incompatibel zijn met uw aangepaste modules of modules van partners en de Umbraco Core-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c2720-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="c2720-285">Hier vindt u aanbevolen procedures:</span><span class="sxs-lookup"><span data-stu-id="c2720-285">Here are best practices:</span></span>

* <span data-ttu-id="c2720-286">Maak altijd een back-up van uw web-app en database voordat u een upgrade.</span><span class="sxs-lookup"><span data-stu-id="c2720-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="c2720-287">Op web-apps in Azure, kunt u automatische back-ups instellen voor uw websites met behulp van de back-up en herstellen van uw site indien nodig met behulp van de functie voor het terugzetten.</span><span class="sxs-lookup"><span data-stu-id="c2720-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="c2720-288">Zie voor meer informatie [reservekopie maken van uw web-app](web-sites-backup.md) en [het herstellen van uw web-app](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="c2720-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="c2720-289">Controleer of de pakketten van partners compatibel met de versie die u een uitvoert zijn naar upgrade.</span><span class="sxs-lookup"><span data-stu-id="c2720-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="c2720-290">Pagina voor het pakket te downloaden, controleert u de compatibiliteit van het project met Umbraco CMS-versie.</span><span class="sxs-lookup"><span data-stu-id="c2720-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="c2720-291">Voor meer informatie over het bijwerken van uw web-app lokaal [raadpleegt u de algemene upgraderichtlijnen](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="c2720-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="c2720-292">Na de upgrade van uw lokale ontwikkelingssite publiceert u de wijzigingen aan de staging-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="c2720-293">Uw toepassing testen.</span><span class="sxs-lookup"><span data-stu-id="c2720-293">Test your application.</span></span> <span data-ttu-id="c2720-294">Als alle er goed uitziet, gebruikt u de **wisselen** knop wisselen van de staging-site naar de productie-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2720-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="c2720-295">Wanneer u gebruikt de **wisselen** bewerking, kunt u de wijzigingen die worden beïnvloed weergeven in uw web-app-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c2720-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="c2720-296">Dit **wisselen** bewerking wisselt de web-apps en -databases.</span><span class="sxs-lookup"><span data-stu-id="c2720-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="c2720-297">Na de **wisselen**, de productie-web-app verwijst naar de database umbraco-fase-db en het tijdelijke web-app verwijst naar umbraco-prod-db-database.</span><span class="sxs-lookup"><span data-stu-id="c2720-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Voorbeeld voor het implementeren van Umbraco CMS wisselen](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="c2720-299">Hier volgen de voordelen van het wisselen van zowel de web-app als de database:</span><span class="sxs-lookup"><span data-stu-id="c2720-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="c2720-300">U kunt terugkeren naar de vorige versie van uw web-app met een andere **wisselen** als er toepassingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="c2720-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="c2720-301">Voor een upgrade moet u voor het implementeren van bestanden en de databases van de tijdelijke web-app in de web-app voor productie en de database.</span><span class="sxs-lookup"><span data-stu-id="c2720-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="c2720-302">Groot aantal dingen kunnen fout gaan wanneer u bestanden en databases implementeert.</span><span class="sxs-lookup"><span data-stu-id="c2720-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="c2720-303">Met behulp van de **wisselen** functie sleuven, we kunnen de uitvaltijd beperken tijdens een upgrade en vermindert het risico van fouten die zich voordoen kunnen bij het implementeren van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c2720-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="c2720-304">U kunt doen **A / B-tests** met behulp van de [testen in productie](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) functie.</span><span class="sxs-lookup"><span data-stu-id="c2720-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="c2720-305">In dit voorbeeld ziet u de flexibiliteit van het platform waarop u aangepaste modules die vergelijkbaar is met de module voor het beheren van de implementatie in omgevingen Umbraco Courier kunt samenstellen.</span><span class="sxs-lookup"><span data-stu-id="c2720-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="c2720-306">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="c2720-306">References</span></span>
[<span data-ttu-id="c2720-307">Flexibele software ontwikkelen met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c2720-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="c2720-308">Faseringsomgevingen voor web-apps in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="c2720-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="c2720-309">Het blokkeren van webtoegang tot niet-productieve implementatiesites</span><span class="sxs-lookup"><span data-stu-id="c2720-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
