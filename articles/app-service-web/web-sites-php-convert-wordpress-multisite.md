---
title: aaaConvert WordPress tooMultisite in Azure App Service
description: Meer informatie over hoe tootake een bestaande WordPress-web-app via Hallo-galerie in Azure is gemaakt en converteert u deze tooWordPress implementatie voor meerdere locaties
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
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a><span data-ttu-id="7d12f-103">Converteren van WordPress tooMultisite in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7d12f-103">Convert WordPress tooMultisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="7d12f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7d12f-104">Overview</span></span>
<span data-ttu-id="7d12f-105">*Door [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="7d12f-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="7d12f-106">In deze zelfstudie leert u hoe tootake een bestaande WordPress-web-app gemaakt door de galerie Hallo in Azure en omzetten in een implementatie voor meerdere locaties WordPress installeren.</span><span class="sxs-lookup"><span data-stu-id="7d12f-106">In this tutorial, you will learn how tootake an existing WordPress web app created through hello gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="7d12f-107">Bovendien leert u hoe tooassign een aangepast domein tooeach Hallo subsites in de installatie.</span><span class="sxs-lookup"><span data-stu-id="7d12f-107">Additionally, you will learn how tooassign a custom domain tooeach of hello subsites within your install.</span></span>

<span data-ttu-id="7d12f-108">Ervan wordt uitgegaan dat u een bestaande installatie van WordPress hebt.</span><span class="sxs-lookup"><span data-stu-id="7d12f-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="7d12f-109">Als u dit niet doet, volgt u Hallo richtlijn voor formaatbepaling in [een WordPress-website uit de galerie Hallo in Azure maken][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="7d12f-109">If you do not, please follow hello guidance provided in [Create a WordPress web site from hello gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="7d12f-110">Converteren van een bestaande WordPress tooMultisite van één site-installatie wordt doorgaans redelijk eenvoudig en veel van Hallo eerste stappen die hier afkomstig zijn direct van Hallo [maken van een netwerk] [ wordpress-codex-create-a-network] pagina op Hallo [WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="7d12f-110">Converting an existing WordPress single site install tooMultisite is generally fairly simple, and many of hello initial steps here come straight from hello [Create A Network][wordpress-codex-create-a-network] page on hello [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="7d12f-111">Aan de slag.</span><span class="sxs-lookup"><span data-stu-id="7d12f-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="7d12f-112">Implementatie voor meerdere locaties toestaan</span><span class="sxs-lookup"><span data-stu-id="7d12f-112">Allow Multisite</span></span>
<span data-ttu-id="7d12f-113">U moet eerst tooenable implementatie voor meerdere locaties via Hallo `wp-config.php` bestand Hello **WP\_toestaan\_implementatie voor meerdere locaties** constante.</span><span class="sxs-lookup"><span data-stu-id="7d12f-113">You first need tooenable Multisite through hello `wp-config.php` file with hello **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="7d12f-114">Er zijn twee methoden tooedit uw web-app-bestanden: Hallo wordt eerst via de FTP- en Hallo tweede via Git.</span><span class="sxs-lookup"><span data-stu-id="7d12f-114">There are two methods tooedit your web app files: hello first is through FTP, and hello second through Git.</span></span> <span data-ttu-id="7d12f-115">Als u niet bekend met het bent toosetup van deze methoden Raadpleeg toohello volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="7d12f-115">If you are unfamiliar with how toosetup either of these methods, please refer toohello following tutorials:</span></span>

* <span data-ttu-id="7d12f-116">[PHP-website met de MySQL- en FTP-][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="7d12f-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="7d12f-117">[PHP-website met de MySQL en Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="7d12f-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="7d12f-118">Open Hallo `wp-config.php` -bestand met de Hallo-editor van uw keuze en voeg de volgende Hallo hierboven Hallo `/* That's all, stop editing! Happy blogging. */` regel.</span><span class="sxs-lookup"><span data-stu-id="7d12f-118">Open hello `wp-config.php` file with hello editor of your choosing and add hello following above hello `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="7d12f-119">Of toosave Hallo het bestand zijn en upload het vorige toohello server!</span><span class="sxs-lookup"><span data-stu-id="7d12f-119">Be sure toosave hello file and upload it back toohello server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="7d12f-120">Netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="7d12f-120">Network Setup</span></span>
<span data-ttu-id="7d12f-121">Meld u bij toohello *wp-beheerder* ruimte van uw web-app en u ziet een nieuw item onder Hallo **hulpprogramma's** menu aangeroepen **netwerk instellen**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-121">Log in toohello *wp-admin* area of your web app and you should see a new item under hello **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="7d12f-122">Klik op **netwerkinstellingen** en vul Hallo details van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7d12f-122">Click **Network Setup** and fill in hello details of your network.</span></span>

![Scherm voor het netwerk instellen][wordpress-network-setup]

<span data-ttu-id="7d12f-124">Deze zelfstudie wordt gebruikgemaakt van Hallo *submappen* schema site omdat deze altijd werkt en we om de aangepaste domeinen van de bovenliggende verderop in de zelfstudie Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-124">This tutorial uses hello *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in hello tutorial.</span></span> <span data-ttu-id="7d12f-125">Deze moet echter mogelijk toosetup een subdomein installeren als u een domein via Hallo toewijst [Azure Portal](https://portal.azure.com) en jokerteken DNS correct setup.</span><span class="sxs-lookup"><span data-stu-id="7d12f-125">However, it should be possible toosetup a subdomain install if you map a domain through hello [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="7d12f-126">Submap instellingen Zie voor meer informatie over het subdomein tegenover Hallo [soorten multisiteconfiguratie] [ wordpress-codex-types-of-networks] artikel op Hallo WordPress Codex.</span><span class="sxs-lookup"><span data-stu-id="7d12f-126">For more information on sub-domain vs sub-directory setups see hello [Types of multisite network][wordpress-codex-types-of-networks] article on hello WordPress Codex.</span></span>

## <a name="enable-hello-network"></a><span data-ttu-id="7d12f-127">Hallo netwerk inschakelen</span><span class="sxs-lookup"><span data-stu-id="7d12f-127">Enable hello Network</span></span>
<span data-ttu-id="7d12f-128">Hallo-netwerk is nu geconfigureerd in de database hello, maar er is een resterende stap tooenable Hallo netwerkfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="7d12f-128">hello network is now configured in hello database, but there is one remaining step tooenable hello network functionality.</span></span> <span data-ttu-id="7d12f-129">Hallo voltooien `wp-config.php` instellingen en zorg ervoor dat `web.config` correct routeert elke site.</span><span class="sxs-lookup"><span data-stu-id="7d12f-129">Finalize hello `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="7d12f-130">Wanneer u op Hallo **installeren** knop op Hallo *netwerkinstellingen* pagina WordPress probeert tooupdate hello `wp-config.php` en `web.config` bestanden.</span><span class="sxs-lookup"><span data-stu-id="7d12f-130">After clicking hello **Install** button on hello *Network Setup* page, WordPress will attempt tooupdate hello `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="7d12f-131">U moet echter altijd controleren Hallo bestanden tooensure Hallo updates met succes zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d12f-131">However, you should always check hello files tooensure hello updates were successful.</span></span> <span data-ttu-id="7d12f-132">Als dat niet het geval is, wordt dit scherm u Hallo vereiste updates worden aangeboden.</span><span class="sxs-lookup"><span data-stu-id="7d12f-132">If not, this screen will present you with hello necessary updates.</span></span> <span data-ttu-id="7d12f-133">Bewerk en Hallo bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="7d12f-133">Edit and save hello files.</span></span>

<span data-ttu-id="7d12f-134">Na het maken wordt deze updates moet u toolog af en meld back in Hallo wp-beheerder dashboard.</span><span class="sxs-lookup"><span data-stu-id="7d12f-134">After making these updates you will need toolog out and log back into hello wp-admin dashboard.</span></span>

<span data-ttu-id="7d12f-135">Er worden nu een menu Extra op Hallo beheerder balk met het label **Mijn Sites**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-135">There should now be an additional menu on hello admin bar labeled **My Sites**.</span></span> <span data-ttu-id="7d12f-136">Dit menu kunt u toocontrol uw nieuwe netwerk via Hallo **netwerk Admin** dashboard.</span><span class="sxs-lookup"><span data-stu-id="7d12f-136">This menu allows you toocontrol your new network through hello **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="7d12f-137">Toevoegen van aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="7d12f-137">Adding custom domains</span></span>
<span data-ttu-id="7d12f-138">Hallo [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] invoegtoepassing kunt u een eenvoudig tooadd aangepaste domeinen tooany site in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="7d12f-138">hello [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze tooadd custom domains tooany site in your network.</span></span> <span data-ttu-id="7d12f-139">Voor Hallo invoegtoepassing toooperate goed is, moet u toodo enkele aanvullende instellingen op Hallo Portal en bij uw domeinregistrar.</span><span class="sxs-lookup"><span data-stu-id="7d12f-139">In order for hello plugin toooperate properly, you need toodo some additional setup on hello Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-toohello-web-app"></a><span data-ttu-id="7d12f-140">Domein toewijzing toohello web-app inschakelen</span><span class="sxs-lookup"><span data-stu-id="7d12f-140">Enable domain mapping toohello web app</span></span>
<span data-ttu-id="7d12f-141">Hallo **vrije** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan modus biedt geen ondersteuning voor het toevoegen van aangepaste domeinen tooWeb Apps.</span><span class="sxs-lookup"><span data-stu-id="7d12f-141">hello **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains tooWeb Apps.</span></span> <span data-ttu-id="7d12f-142">U moet tooswitch te**gedeelde** of **standaard** modus.</span><span class="sxs-lookup"><span data-stu-id="7d12f-142">You will need tooswitch too**Shared** or **Standard** mode.</span></span> <span data-ttu-id="7d12f-143">toodo dit:</span><span class="sxs-lookup"><span data-stu-id="7d12f-143">toodo this:</span></span>

* <span data-ttu-id="7d12f-144">Meld u bij toohello Azure-Portal en zoek uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7d12f-144">Log in toohello Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="7d12f-145">Klik op Hallo **opschalen** tabblad **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-145">Click on hello **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="7d12f-146">Onder **algemene**, selecteert u *gedeelde* of *STANDARD*</span><span class="sxs-lookup"><span data-stu-id="7d12f-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="7d12f-147">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="7d12f-147">Click **Save**</span></span>

<span data-ttu-id="7d12f-148">U kunt wordt een bericht weergegeven waarin u wordt gevraagd tooverify Hallo wijzigen en uw web-app kan nu een kosten, afhankelijk van het gebruik in rekening gebracht en andere configuratieset Hallo bevestigen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-148">You may receive a message asking you tooverify hello change and acknowledge your web app may now incur a cost, depending upon usage and hello other configuration you set.</span></span>

<span data-ttu-id="7d12f-149">Het duurt een paar seconden tooprocess Hallo nieuwe instellingen, is dit nu een goed moment toostart-instellen van uw domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-149">It takes a few seconds tooprocess hello new settings, so now is a good time toostart setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="7d12f-150">Verifieer uw domein</span><span class="sxs-lookup"><span data-stu-id="7d12f-150">Verify your domain</span></span>
<span data-ttu-id="7d12f-151">Voordat u Azure Web Apps kunt u de site van een domein toohello toomap, moet u eerst tooverify Hallo autorisatie toomap Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-151">Before Azure Web Apps will allow you toomap a domain toohello site, you first need tooverify that you have hello authorization toomap hello domain.</span></span> <span data-ttu-id="7d12f-152">toodo geval is, moet u een nieuwe CNAME-record tooyour DNS-vermelding toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-152">toodo so, you must add a new CNAME record tooyour DNS entry.</span></span>

* <span data-ttu-id="7d12f-153">Aanmelden van tooyour domein-DNS-beheer</span><span class="sxs-lookup"><span data-stu-id="7d12f-153">Log in tooyour domain's DNS manager</span></span>
* <span data-ttu-id="7d12f-154">Maakt een nieuwe CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="7d12f-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="7d12f-155">Punt *awverify* te*awverify. YOUR_DOMAIN.azurewebsites.NET*</span><span class="sxs-lookup"><span data-stu-id="7d12f-155">Point *awverify* too*awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="7d12f-156">Het kan even duren om Hallo DNS-wijzigingen toogo volledige kracht, dus als Hallo stappen werken niet onmiddellijk, gaat u koffie, maken en vervolgens keert u terug en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7d12f-156">It may take some time for hello DNS changes toogo into full effect, so if hello following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-hello-domain-toohello-web-app"></a><span data-ttu-id="7d12f-157">Hallo domein toohello web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d12f-157">Add hello domain toohello web app</span></span>
<span data-ttu-id="7d12f-158">Retour tooyour web-app via hello Azure-Portal klikt u op **instellingen**, en klik vervolgens op **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-158">Return tooyour web app through hello Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="7d12f-159">Wanneer Hallo *SSL-instellingen* worden weergegeven, ziet u Hallo velden waar u invoer op alle Hallo-domeinen die u wenst dat tooassign tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="7d12f-159">When hello *SSL settings* are displayed, you will see hello fields where you will input all hello domains which you wish tooassign tooyour web app.</span></span> <span data-ttu-id="7d12f-160">Als een domein is hier niet worden vermeld, is het niet mogelijk voor de toewijzing binnen WordPress, ongeacht hoe Hallo domein-DNS ingesteld is.</span><span class="sxs-lookup"><span data-stu-id="7d12f-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how hello domain DNS is setup.</span></span>

![Dialoogvenster aangepaste domeinen beheren][wordpress-manage-domains]

<span data-ttu-id="7d12f-162">Nadat u uw domein in het tekstvak hello te typen, controleert Azure Hallo CNAME-record die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d12f-162">After typing your domain into hello text box, Azure will verify hello CNAME record you created previously.</span></span> <span data-ttu-id="7d12f-163">Als Hallo DNS is niet volledig is doorgegeven, wordt een rode indicator wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d12f-163">If hello DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="7d12f-164">Als deze voltooid is, ziet u een groen vinkje.</span><span class="sxs-lookup"><span data-stu-id="7d12f-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="7d12f-165">Let op Hallo die IP-adres onder Hallo van Hallo dialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7d12f-165">Take note of hello IP Address listed at hello bottom of hello dialog.</span></span> <span data-ttu-id="7d12f-166">U moet deze toosetup Hallo een record voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-166">You will need this toosetup hello A record for your domain.</span></span>

## <a name="setup-hello-domain-a-record"></a><span data-ttu-id="7d12f-167">Hallo domein A-record instellen</span><span class="sxs-lookup"><span data-stu-id="7d12f-167">Setup hello domain A record</span></span>
<span data-ttu-id="7d12f-168">U kunt hello andere stappen is gelukt, nu Hallo domein tooyour Azure-web-app via een DNS A-record te toewijzen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-168">If hello other steps were successful, you may now assign hello domain tooyour Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="7d12f-169">Het is belangrijk toonote hier die Azure-web-apps worden geaccepteerd CNAME zowel A-records, maar u *moet* een toewijzing van een record tooenable juiste domein gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7d12f-169">It is important toonote here that Azure web apps accept both CNAME and A records, however you *must* use an A record tooenable proper domain mapping.</span></span> <span data-ttu-id="7d12f-170">Worden een CNAME kan niet doorgestuurd tooanother CNAME, dit is wat Azure met YOUR_DOMAIN.azurewebsites.net voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d12f-170">A CNAME cannot be forwarded tooanother CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="7d12f-171">Met de Hallo IP-adres van de vorige stap hello, retourneren tooyour DNS-beheer en setup Hallo een record toopoint toothat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7d12f-171">Using hello IP address from hello previous step, return tooyour DNS manager and setup hello A record toopoint toothat IP.</span></span>

## <a name="install-and-setup-hello-plugin"></a><span data-ttu-id="7d12f-172">Installeren en instellen Hallo-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="7d12f-172">Install and setup hello plugin</span></span>
<span data-ttu-id="7d12f-173">Implementatie voor meerdere locaties WordPress nog momenteel geen gebruikmaakt van een ingebouwde methode toomap aangepaste domeinen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-173">WordPress Multisite currently does not have a built-in method toomap custom domains.</span></span> <span data-ttu-id="7d12f-174">Er is echter een invoegtoepassing aangeroepen [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] waarmee Hallo functionaliteit toegevoegd voor u.</span><span class="sxs-lookup"><span data-stu-id="7d12f-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds hello functionality for you.</span></span> <span data-ttu-id="7d12f-175">Meld u bij toohello netwerk Admin deel van uw site en installeer Hallo **WordPress MU domein toewijzing** invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="7d12f-175">Log in toohello Network Admin portion of your site and install hello **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="7d12f-176">Nadat het installeren en activeren van de invoegtoepassing hello, gaat u naar **instellingen** > **domein toewijzing** tooconfigure Hallo-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="7d12f-176">After installing and activating hello plugin, visit **Settings** > **Domain Mapping** tooconfigure hello plugin.</span></span> <span data-ttu-id="7d12f-177">In de eerste tekstvak hello, *IP-adres*, invoer Hallo IP-adres gebruikt van toosetup Hallo een record voor Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-177">In hello first textbox, *Server IP Address*, input hello IP Address you used toosetup hello A record for hello domain.</span></span> <span data-ttu-id="7d12f-178">Stel een *Domeinopties* u wenst (Hallo zijn standaard vaak fijn) en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-178">Set any *Domain Options* you desire (hello defaults are often fine) and click **Save**.</span></span>

## <a name="map-hello-domain"></a><span data-ttu-id="7d12f-179">Hallo domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="7d12f-179">Map hello domain</span></span>
<span data-ttu-id="7d12f-180">Ga naar Hallo **Dashboard** voor Hallo-site die u wenst toomap Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-180">Visit hello **Dashboard** for hello site you wish toomap hello domain to.</span></span> <span data-ttu-id="7d12f-181">Klik op **extra** > **domein toewijzing** en type Hallo nieuw domein in Hallo tekstvak en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7d12f-181">Click on **Tools** > **Domain Mapping** and type hello new domain into hello textbox and click **Add**.</span></span>

<span data-ttu-id="7d12f-182">Standaard wordt het nieuwe domein Hallo herschreven toohello automatisch gegenereerde site domein te zijn.</span><span class="sxs-lookup"><span data-stu-id="7d12f-182">By default, hello new domain will be rewritten toohello autogenerated site domain.</span></span> <span data-ttu-id="7d12f-183">Als u wilt dat toohave alle verkeer dat wordt verzonden toohello nieuw domein, controleert u Hallo *primair domein voor deze blog* vak voordat u opslaat.</span><span class="sxs-lookup"><span data-stu-id="7d12f-183">If you want toohave all traffic sent toohello new domain, check hello *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="7d12f-184">U kunt een onbeperkt aantal domeinen tooa site toevoegen, maar slechts één primaire kan zijn.</span><span class="sxs-lookup"><span data-stu-id="7d12f-184">You can add an unlimited number of domains tooa site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="7d12f-185">Opnieuw doen</span><span class="sxs-lookup"><span data-stu-id="7d12f-185">Do it again</span></span>
<span data-ttu-id="7d12f-186">Azure-Web-Apps kunt u tooadd een onbeperkt aantal domeinen tooa web-app.</span><span class="sxs-lookup"><span data-stu-id="7d12f-186">Azure Web Apps allow you tooadd an unlimited number of domains tooa web app.</span></span> <span data-ttu-id="7d12f-187">tooadd een ander domein, moet u tooexecute hello **Verifieer uw domein** en **Setup Hallo domein A-record** secties voor elk domein.</span><span class="sxs-lookup"><span data-stu-id="7d12f-187">tooadd another domain you will need tooexecute hello **Verify your domain** and **Setup hello domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="7d12f-188">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="7d12f-188">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7d12f-189">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="7d12f-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="7d12f-190">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="7d12f-190">What's changed</span></span>
* <span data-ttu-id="7d12f-191">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7d12f-191">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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


