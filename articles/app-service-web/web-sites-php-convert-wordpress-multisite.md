---
title: WordPress converteren naar meerdere locaties in Azure App Service
description: Meer informatie over het maken van een bestaande web-app voor WordPress is gemaakt door de galerie in Azure en converteren naar WordPress implementatie voor meerdere locaties
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="ef681-103">WordPress converteren naar meerdere locaties in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ef681-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="ef681-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ef681-104">Overview</span></span>
<span data-ttu-id="ef681-105">*Door [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="ef681-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="ef681-106">In deze zelfstudie leert u een bestaande web-app voor WordPress is gemaakt door de galerie in Azure maken en deze omzetten in een implementatie voor meerdere locaties WordPress-installatie.</span><span class="sxs-lookup"><span data-stu-id="ef681-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="ef681-107">Bovendien leert u hoe u een aangepast domein toewijzen aan elk van de subsites binnen uw installatie.</span><span class="sxs-lookup"><span data-stu-id="ef681-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="ef681-108">Ervan wordt uitgegaan dat u een bestaande installatie van WordPress hebt.</span><span class="sxs-lookup"><span data-stu-id="ef681-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="ef681-109">Volg de richtlijnen als u dit niet doet, [een WordPress-website maken vanuit de Azure-galerie][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="ef681-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="ef681-110">Converteren van een bestaande WordPress één site installeren op meerdere locaties is doorgaans redelijk eenvoudig en veel van de eerste stappen die hier worden geleverd rechtstreeks vanuit de [maken van een netwerk] [ wordpress-codex-create-a-network] pagina op de [ WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="ef681-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="ef681-111">Aan de slag.</span><span class="sxs-lookup"><span data-stu-id="ef681-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="ef681-112">Implementatie voor meerdere locaties toestaan</span><span class="sxs-lookup"><span data-stu-id="ef681-112">Allow Multisite</span></span>
<span data-ttu-id="ef681-113">U moet eerst meerdere locaties via inschakelen de `wp-config.php` het bestand met de **WP\_toestaan\_implementatie voor meerdere locaties** constante.</span><span class="sxs-lookup"><span data-stu-id="ef681-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="ef681-114">Er zijn twee methoden voor het bewerken van uw web-app-bestanden: de eerste is via de FTP- en de tweede via Git.</span><span class="sxs-lookup"><span data-stu-id="ef681-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="ef681-115">Als u niet bekend met het instellen van deze methoden bent, raadpleegt u de volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="ef681-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="ef681-116">[PHP-website met de MySQL- en FTP-][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="ef681-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="ef681-117">[PHP-website met de MySQL en Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="ef681-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="ef681-118">Open de `wp-config.php` -bestand met een editor van uw keuze en voeg de volgende bovenstaande de `/* That's all, stop editing! Happy blogging. */` regel.</span><span class="sxs-lookup"><span data-stu-id="ef681-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="ef681-119">Zorg dat het bestand opslaan en upload het naar de server!</span><span class="sxs-lookup"><span data-stu-id="ef681-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="ef681-120">Netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="ef681-120">Network Setup</span></span>
<span data-ttu-id="ef681-121">Meld u aan bij de *wp-beheerder* ruimte van uw web-app en u ziet een nieuw item onder de **extra** menu aangeroepen **netwerkinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ef681-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="ef681-122">Klik op **netwerkinstellingen** en vult u de details van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef681-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Scherm voor het netwerk instellen][wordpress-network-setup]

<span data-ttu-id="ef681-124">Deze zelfstudie wordt gebruikgemaakt van de *submappen* schema site omdat deze altijd werkt en we om de aangepaste domeinen van de bovenliggende verderop in de zelfstudie instellen.</span><span class="sxs-lookup"><span data-stu-id="ef681-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="ef681-125">Echter, moet het mogelijk installatie van een subdomein installeren als u een domein via toewijzen voor de [Azure Portal](https://portal.azure.com) en jokerteken DNS correct setup.</span><span class="sxs-lookup"><span data-stu-id="ef681-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="ef681-126">Zie voor meer informatie over het subdomein tegenover submap instellingen de [soorten multisiteconfiguratie] [ wordpress-codex-types-of-networks] artikel op de WordPress-Codex.</span><span class="sxs-lookup"><span data-stu-id="ef681-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="ef681-127">Het netwerk inschakelen</span><span class="sxs-lookup"><span data-stu-id="ef681-127">Enable the Network</span></span>
<span data-ttu-id="ef681-128">Het netwerk is nu geconfigureerd in de database, maar er is een resterende stap in het inschakelen van de netwerkfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="ef681-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="ef681-129">Voltooi de `wp-config.php` instellingen en zorg ervoor dat `web.config` goed routeert elke site.</span><span class="sxs-lookup"><span data-stu-id="ef681-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="ef681-130">Wanneer u op de **installeren** knop op de *netwerkinstellingen* pagina WordPress probeert bij te werken de `wp-config.php` en `web.config` bestanden.</span><span class="sxs-lookup"><span data-stu-id="ef681-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="ef681-131">U moet echter altijd de bestanden om te controleren of dat de updates met succes zijn controleren.</span><span class="sxs-lookup"><span data-stu-id="ef681-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="ef681-132">Als dit niet het geval is, wordt dit scherm u met de vereiste updates worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ef681-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="ef681-133">Bewerken en opslaan van de bestanden.</span><span class="sxs-lookup"><span data-stu-id="ef681-133">Edit and save the files.</span></span>

<span data-ttu-id="ef681-134">Nadat u back deze updates u moet af en meld in het dashboard wp-beheerder.</span><span class="sxs-lookup"><span data-stu-id="ef681-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="ef681-135">Er worden nu een menu Extra op de admin-balk met het label **Mijn Sites**.</span><span class="sxs-lookup"><span data-stu-id="ef681-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="ef681-136">Dit menu kunt u bepalen van uw nieuwe netwerk via de **netwerk Admin** dashboard.</span><span class="sxs-lookup"><span data-stu-id="ef681-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="ef681-137">Toevoegen van aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="ef681-137">Adding custom domains</span></span>
<span data-ttu-id="ef681-138">De [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] invoegtoepassing kunt u probleemloos aangepaste domeinen toevoegen aan een site in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="ef681-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="ef681-139">Voor de invoegtoepassing correcte werking moet, u enkele aanvullende instellingen op de Portal en bij uw domeinregistrar doen.</span><span class="sxs-lookup"><span data-stu-id="ef681-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="ef681-140">Domein toewijzen aan de web-app</span><span class="sxs-lookup"><span data-stu-id="ef681-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="ef681-141">De **vrije** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan modus biedt geen ondersteuning voor het toevoegen van aangepaste domeinen aan Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="ef681-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="ef681-142">U moet overschakelen naar **gedeelde** of **standaard** modus.</span><span class="sxs-lookup"><span data-stu-id="ef681-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="ef681-143">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="ef681-143">To do this:</span></span>

* <span data-ttu-id="ef681-144">Aanmelden bij de Azure-Portal en zoek uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ef681-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="ef681-145">Klik op de **opschalen** tabblad **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ef681-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="ef681-146">Onder **algemene**, selecteert u *gedeelde* of *STANDARD*</span><span class="sxs-lookup"><span data-stu-id="ef681-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="ef681-147">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="ef681-147">Click **Save**</span></span>

<span data-ttu-id="ef681-148">U wordt gevraagd om te controleren of de wijziging en bevestigt dat uw web-app kan nu kosten in rekening gebracht een, al naar gelang het verbruik en de andere configuratie die u instelt.</span><span class="sxs-lookup"><span data-stu-id="ef681-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="ef681-149">Het duurt een paar seconden voor het verwerken van de nieuwe instellingen is nu een goed moment om het instellen van uw domein te starten.</span><span class="sxs-lookup"><span data-stu-id="ef681-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="ef681-150">Verifieer uw domein</span><span class="sxs-lookup"><span data-stu-id="ef681-150">Verify your domain</span></span>
<span data-ttu-id="ef681-151">Voordat u Azure Web Apps kunt u een domein worden toegewezen aan de site, moet u eerst controleren of u de autorisatie hebt voor het toewijzen van het domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="ef681-152">Om dit te doen, moet u een nieuwe CNAME-record toevoegen aan uw DNS-vermelding.</span><span class="sxs-lookup"><span data-stu-id="ef681-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="ef681-153">Aanmelden bij uw domein-DNS-beheer</span><span class="sxs-lookup"><span data-stu-id="ef681-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="ef681-154">Maakt een nieuwe CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="ef681-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="ef681-155">Punt *awverify* naar *awverify. YOUR_DOMAIN.azurewebsites.NET*</span><span class="sxs-lookup"><span data-stu-id="ef681-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="ef681-156">Het kan even duren voordat de DNS-wijzigingen van kracht volledige, dus als u de volgende stappen werken niet onmiddellijk gaat koffie, maken en vervolgens keert u terug en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ef681-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="ef681-157">Het domein toevoegen aan de web-app</span><span class="sxs-lookup"><span data-stu-id="ef681-157">Add the domain to the web app</span></span>
<span data-ttu-id="ef681-158">Ga terug naar uw web-app via de Azure-Portal, klikt u op **instellingen**, en klik vervolgens op **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="ef681-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="ef681-159">Wanneer de *SSL-instellingen* worden weergegeven, ziet u de velden waar u invoer op alle domeinen die u wilt toewijzen aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ef681-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="ef681-160">Als een domein is hier niet worden vermeld, is het niet mogelijk voor de toewijzing binnen WordPress, ongeacht hoe de domein-DNS ingesteld is.</span><span class="sxs-lookup"><span data-stu-id="ef681-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Dialoogvenster aangepaste domeinen beheren][wordpress-manage-domains]

<span data-ttu-id="ef681-162">Nadat u uw domein in het tekstvak te typen, Azure controleert of de CNAME-record dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef681-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="ef681-163">Als de DNS-server is niet volledig is doorgegeven, wordt een rode indicator wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef681-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="ef681-164">Als deze voltooid is, ziet u een groen vinkje.</span><span class="sxs-lookup"><span data-stu-id="ef681-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="ef681-165">Let op het IP-adres aan de onderkant van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef681-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="ef681-166">U moet dit voor het instellen van de A-record voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="ef681-167">Instellen van het domein een record</span><span class="sxs-lookup"><span data-stu-id="ef681-167">Setup the domain A record</span></span>
<span data-ttu-id="ef681-168">Als de andere stappen voltooid zijn, kunt u kunt nu het domein toewijzen aan uw Azure-web-app in een DNS A-record.</span><span class="sxs-lookup"><span data-stu-id="ef681-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="ef681-169">Het is belangrijk te weten hier die Azure-web-apps worden geaccepteerd CNAME zowel A-records, maar u *moet* gebruikmaken van een A-record voor de toewijzing van het juiste domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="ef681-170">Een CNAME kan niet worden doorgestuurd naar een andere CNAME, dit is wat Azure met YOUR_DOMAIN.azurewebsites.net voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef681-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="ef681-171">Met behulp van het IP-adres van de vorige stap, terug naar uw DNS-beheer en de A-record wijst u aan dat IP-adres instellen.</span><span class="sxs-lookup"><span data-stu-id="ef681-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="ef681-172">Installeren en instellen van de invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="ef681-172">Install and setup the plugin</span></span>
<span data-ttu-id="ef681-173">Implementatie voor meerdere locaties WordPress heeft momenteel geen ingebouwde methode om toe te wijzen van aangepaste domeinen.</span><span class="sxs-lookup"><span data-stu-id="ef681-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="ef681-174">Er is echter een invoegtoepassing aangeroepen [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] waarmee de functionaliteit voor u worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ef681-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="ef681-175">Aanmelden bij het netwerk Admin-gedeelte van uw site en installeer de **WordPress MU domein toewijzing** invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ef681-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="ef681-176">Na het installeren en activeren van de invoegtoepassing, gaat u naar **instellingen** > **domein toewijzing** voor het configureren van de invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ef681-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="ef681-177">In het eerste tekstvak *IP-adres*, voer het IP-adres dat u gebruikt voor het instellen van de A-record voor het domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="ef681-178">Stel een *Domeinopties* u desire (de standaardwaarden zijn vaak fijn) en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ef681-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="ef681-179">Het domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="ef681-179">Map the domain</span></span>
<span data-ttu-id="ef681-180">Ga naar de **Dashboard** voor de site die u wilt toewijzen van het domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="ef681-181">Klik op **extra** > **domein toewijzing** en typt u het nieuwe domein in het tekstvak en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ef681-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="ef681-182">Standaard wordt het nieuwe domein worden herschreven aan het domein van de site automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ef681-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="ef681-183">Als u wilt dat alle verkeer dat wordt verzonden naar het nieuwe domein, Controleer de *primair domein voor deze blog* vak voordat u opslaat.</span><span class="sxs-lookup"><span data-stu-id="ef681-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="ef681-184">U kunt een onbeperkt aantal domeinen toevoegen aan een site, maar slechts één primaire kan zijn.</span><span class="sxs-lookup"><span data-stu-id="ef681-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="ef681-185">Opnieuw doen</span><span class="sxs-lookup"><span data-stu-id="ef681-185">Do it again</span></span>
<span data-ttu-id="ef681-186">Azure-Web-Apps kunt u een onbeperkt aantal domeinen toevoegen aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="ef681-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="ef681-187">Toevoegen van een ander domein, moet u uitvoeren van de **Verifieer uw domein** en **instellen van het domein een record** secties voor elk domein.</span><span class="sxs-lookup"><span data-stu-id="ef681-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="ef681-188">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="ef681-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ef681-189">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="ef681-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ef681-190">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="ef681-190">What's changed</span></span>
* <span data-ttu-id="ef681-191">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ef681-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


