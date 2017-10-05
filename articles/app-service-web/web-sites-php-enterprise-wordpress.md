---
title: Bedrijfsniveau WordPress in Azure | Microsoft Docs
description: Meer informatie over het hosten van een enterprise-klasse WordPress-site op Azure App Service
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 21281955458a2632d96a91d884cab13803f4d296
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Bedrijfsniveau WordPress in Azure
Azure App Service biedt een omgeving schaalbare, veilige en eenvoudig te gebruiken voor essentiële en grootschalige [WordPress] [ wordpress] sites. Microsoft zelf wordt uitgevoerd bedrijfsniveau sites, zoals de [Office] [ officeblog] en [Bing] [ bingblog] blogs. Dit artikel laat zien hoe u de functie Web Apps van Microsoft Azure App Service kunt instellen en onderhouden van een enterprise-klasse, cloud-gebaseerde WordPress-site die een groot aantal bezoekers kan verwerken.

## <a name="architecture-and-planning"></a>Architectuur en planning
Een basisinstallatie van WordPress heeft slechts twee vereisten:

* **MySQL-Database**: deze vereiste is beschikbaar via [ClearDB in Azure Marketplace][cdbnstore]. Als alternatief kunt u uw eigen MySQL-installatie op Azure Virtual Machines kunt beheren met behulp van [Windows] [ mysqlwindows] of [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB biedt diverse MySQL-configuraties. Elke configuratie heeft verschillende prestatiekenmerken. Zie de [Azure Store] [ cdbnstore] voor meer informatie over de offerings die beschikbaar zijn via de Azure Store of rechtstreeks weergegeven op de [ClearDB website](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 of hoger**: Azure App Service biedt momenteel [versie van PHP 5.4, 5.5 en 5.6][phpwebsite].

  > [!NOTE]
  > Het is raadzaam dat u de nieuwste versie van PHP altijd worden uitgevoerd zodat u de meest recente beveiligingsupdates hebben.
  >
  >

### <a name="basic-deployment"></a>Eenvoudige implementatie
Als u alleen de basisvereisten gebruikt, kunt u een basisoplossing binnen een Azure-regio.

![Een Azure-web-app en MySQL-Database gehost in één Azure-regio][basic-diagram]

Hoewel zo u meerdere exemplaren van de Web-Apps van de site kunt voor het schalen van uw toepassing maken, wordt alles gehost binnen de datacentra in een specifieke geografische regio. Trage responstijden bij gebruik van de site mogelijk ziet u bezoekers buiten deze regio. Als de datacentra in deze regio falen beide, dat geldt ook voor uw toepassing.

### <a name="multi-region-deployment"></a>Implementatie van meerdere landen/regio
Met behulp van Azure [Traffic Manager][trafficmanager], kunt u de schaal van uw WordPress-site voor meerdere geografische regio's en geef dezelfde URL voor alle bezoekers. Alle bezoekers komen via het Traffic Manager en vervolgens doorgestuurd naar een regio die gebaseerd op de configuratie van taakverdeling.

![Een Azure-web-app, gehost in meerdere regio's met hoge beschikbaarheid CDBR router voor het routeren naar MySQL tussen regio 's][multi-region-diagram]

De WordPress-site zou nog steeds worden geschaald over meerdere exemplaren van de Web-Apps in elke regio, maar deze schaling is specifiek voor een regio. Intensief verkeer regio's en regio's weinig verkeer kunnen anders worden uitgebreid.

Als u wilt repliceren en doorsturen van verkeer naar meerdere MySQL-databases, kunt u [ClearDB hoge beschikbaarheid-routers (CDBRs)] [ cleardbscale] (links weergegeven) of [MySQL Cluster Carrier hoogwaardige Edition (CGE)][cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Meerdere landen/regio-implementatie met de Mediaopslag en opslaan in cache
Als de site uploads of mediabestanden van hosts accepteert, gebruikt u Azure Blob-opslag. Als u nodig hebt in cache opslaan, kunt u overwegen [Redis-cache][rediscache], [Memcache Cloud](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), of een van de cache in aanbiedingen in de [Azure Store](http://azure.microsoft.com/gallery/store/).

![Een Azure-web-app, gehost in meerdere regio's met hoge beschikbaarheid CDBR router voor MySQL met beheerde-Cache, Blob-opslag en Content Delivery Network][performance-diagram]

BLOB-opslag is geografisch worden verdeeld over regio's standaard, zodat u niet hoeft te hoeven maken over het repliceren van bestanden op alle sites. U kunt ook inschakelen met de Azure [Content Delivery Network] [ cdn] voor Blob storage, die bestanden distribueert naar knooppunten die zich het dichtst bij uw bezoekers eindigen.

### <a name="planning"></a>Planning
#### <a name="additional-requirements"></a>Aanvullende vereisten
| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **Uploaden of opslaan van grote bestanden** |[WordPress-invoegtoepassing voor het gebruik van Blob-opslag][storageplugin] |
| **E-mail verzenden** |[SendGrid] [ storesendgrid] en de [WordPress-invoegtoepassing voor het gebruik van SendGrid][sendgridplugin] |
| **Aangepaste domeinnamen** |[Een aangepaste domeinnaam configureren in Azure App Service][customdomain] |
| **HTTPS** |[HTTPS inschakelen voor een web-app in Azure App Service][httpscustomdomain] |
| **Validatie van vóór productie** |[Faseringsomgevingen voor web-apps in Azure App Service instellen][staging] <p>Wanneer u een web-app van fasering naar de productie verplaatst, gaat u ook de WordPress-configuratie. Zorg ervoor dat alle instellingen zijn bijgewerkt naar de vereisten voor uw app in productie voordat u de voorbereide app naar productie verplaatsen.</p> |
| **Bewaking en probleemoplossing** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service] [ log] en [Web-Apps bewaken in Azure App Service][monitor] |
| **Uw site implementeren** |[Een web-app in Azure App Service implementeren][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Beschikbaarheid en herstel na noodgevallen
| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **Laden van saldo sites** of **geo-sites distribueren** |[Verkeer leiden met Azure Traffic Manager][trafficmanager] |
| **Back-ups maken en bestanden terugzetten** |[Maak een back-up van een web-app in Azure App Service] [ backup] en [herstellen van een web-app in Azure App Service][restore] |

#### <a name="performance"></a>Prestaties
Prestaties in de cloud wordt bewerkstelligd voornamelijk met caching en scale-out. Echter, moeten het geheugen, bandbreedte en andere kenmerken van het hosten van Web-Apps worden beschouwd.

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **De mogelijkheden van App Service-exemplaar begrijpen** |[Prijsinformatie, met inbegrip van de mogelijkheden van App Service-lagen][websitepricing] |
| **Cache-resources** |[Redis-cache][rediscache], [Memcache Cloud](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), of een van de cache in aanbiedingen in de [Azure Store](/gallery/store/) |
| **Uw toepassing schalen** |[Een web-app schalen in Azure App Service] [ websitescale] en [ClearDB hoge beschikbaarheid routering][cleardbscale]. Als u wilt hosten en beheren van uw eigen MySQL-installatie, kunt u overwegen [MySQL-Cluster CGE] [ cge] voor scale-out. |

#### <a name="migration"></a>Migratie
Er zijn twee methoden voor het migreren van een bestaande WordPress-site naar Azure App Service:

* **[WordPress exporteren][export]**: deze methode exporteert u de inhoud van uw blog. U kunt de inhoud vervolgens importeren in een nieuwe WordPress-site op Azure App Service met behulp van de [importfunctie van WordPress-invoegtoepassing][import].

  > [!NOTE]
  > Tijdens dit proces u uw inhoud migreert kunt, worden deze alle invoegtoepassingen, thema's of andere aanpassingen niet gemigreerd. Deze onderdelen moet u handmatig opnieuw installeren.
  >
  >
* **Handmatige migratie**: [Back-up van uw site] [ wordpressbackup] en [database][wordpressdbbackup], en vervolgens handmatig te herstellen een web-app in Azure App Service en de bijbehorende MySQL-database. Deze methode is handig voor het migreren van maximaal aangepaste sites omdat verspillen handmatig installeren van invoegtoepassingen, thema's en andere aanpassingen wordt voorkomen.

## <a name="step-by-step-instructions"></a>Stapsgewijze instructies
### <a name="create-a-wordpress-site"></a>Een WordPress-site maken
1. Gebruik de [Azure Marketplace] [ cdbnstore] voor het maken van een MySQL-database van de grootte die u hebt geïdentificeerd in de [architectuur en planning](#planning) sectie in de regio of regio's waar u uw site wordt host.
2. Volg de stappen in [een WordPress-web-app maken in Azure App Service] [ createwordpress] voor het maken van een WordPress-web-app. Wanneer u de web-app maakt, selecteert u **gebruik een bestaande MySQL-Database**, en selecteer vervolgens de database die u in stap 1 hebt gemaakt.

Als u van een bestaande WordPress-site migreert, Zie [migreren van een bestaande WordPress-site naar Azure](#Migrate-an-existing-WordPress-site-to-Azure) nadat u een nieuwe web-app hebt gemaakt.

### <a name="migrate-an-existing-wordpress-site-to-azure"></a>Een bestaande WordPress-site migreren naar Azure
Zoals vermeld in de [architectuur en planning](#planning) sectie, er zijn twee manieren voor het migreren van een WordPress-site:

* **Gebruik exporteren en importeren** voor sites die niet veel aanpassingen hebben of alleen waar u de inhoud te verplaatsen.
* **Gebruik back-up en herstel** voor sites met veel aanpassing waarnaar u wilt verplaatsen alles.

Gebruik een van de volgende secties voor het migreren van uw site.

#### <a name="the-export-and-import-method"></a>De methode exporteren en importeren
1. Gebruik [WordPress exporteren] [ export] exporteren van uw bestaande site.
2. Een web-app maken met behulp van de stappen in de [een WordPress-site maken](#Create-a-new-WordPress-site) sectie.
3. Aanmelden bij uw WordPress-site op het [Azure-portal][mgmtportal], en klik vervolgens op **Plugins** > **nieuwe toevoegen**. Zoek en installeer de **WordPress importfunctie** invoegtoepassing.
4. Nadat u de importfunctie van WordPress-invoegtoepassing hebt geïnstalleerd, klikt u op **extra** > **importeren**, en klik vervolgens op **WordPress** de importfunctie van WordPress-invoegtoepassing gebruiken.
5. Op de **importeren WordPress** pagina, klikt u op **bestand kiezen**. Zoek het WXR-bestand dat is geëxporteerd vanuit uw bestaande WordPress-site en klik vervolgens op **uploadbestand en importeer**.
6. Klik op **indienen**. U wordt gevraagd om het importeren is geslaagd.
7. Nadat u al deze stappen hebt voltooid, start opnieuw op uw site uit de **App Services** blade in de [Azure-portal][mgmtportal].

Nadat u de site hebt geïmporteerd, moet u mogelijk de volgende stappen uitvoeren om te schakelen instellingen die niet in het importbestand.

| Als u dit... | Dit doen... |
| --- | --- |
| **Permalinks** |Vanuit de WordPress-dashboard van de nieuwe site, klikt u op **instellingen** > **Permalinks**, en werk vervolgens de Permalinks-structuur. |
| **afbeelding/media koppelingen** |Als koppelingen wilt bijwerken naar de nieuwe locatie, gebruiken de [Velvet blauwe bijwerken URL's invoegtoepassing][velvet], een zoeken en vervangen hulpprogramma of de koppelingen in de database handmatig bijwerken. |
| **Thema 's** |Ga naar **vormgeving** > **thema**, en werk vervolgens de Websitethema indien nodig. |
| **Menu 's** |Als het thema menu's ondersteunt, kan de oude submap ingesloten in ze nog steeds door koppelingen naar de startpagina. Ga naar **vormgeving** > **menu's**, en werk deze bij. |

#### <a name="the-backup-and-restore-method"></a>De methode back-up en herstel
1. Maak een back-up van uw bestaande WordPress-site met behulp van de informatie op [WordPress back-ups][wordpressbackup].
2. Maak een back-up van uw bestaande database met behulp van de informatie op [back-ups van uw database][wordpressdbbackup].
3. Een database maken en herstellen van de back-up.

   1. Koop een nieuwe database vanuit de [Azure Marketplace][cdbnstore], of een MySQL-database instellen op een [Windows] [ mysqlwindows] of [Linux] [ mysqllinux] virtuele machine.
   2. Gebruik een MySQL-client, zoals [MySQL Workbench] [ workbench] verbinding maken met de nieuwe database en uw WordPress-database importeren.
   3. De database als u wilt wijzigen van de vermeldingen van het domein naar het nieuwe domein in de Azure App Service, bijvoorbeeld mywordpress.azurewebsites.net bijwerken. Gebruik de [zoeken en vervangen voor WordPress Databases Script] [ searchandreplace] overal veilig te wijzigen.
4. Een web-app in de Azure portal maken en publiceren van de WordPress back-up.

   1. Maken van een web-app met een database in de [Azure-portal][mgmtportal], klikt u op **nieuw** > **Web en mobiel** > **Azure Marketplace** > **Web-Apps** > **webtoepassing + SQL** (of **webtoepassing + MySQL**) > **maken**. Configureer alle vereiste instellingen voor het maken van een leeg web-app.
   2. Zoek in uw WordPress back-up, de **wp-config.php** bestand en open het in een teksteditor. De volgende vermeldingen vervangen door de gegevens voor uw nieuwe MySQL-database:

      * **DB_NAME**: de gebruikersnaam van de database.
      * **DB_USER**: de naam van de gebruiker gebruikt voor toegang tot de database.
      * **DB_PASSWORD**: het wachtwoord van de gebruiker.

        Nadat u deze items gewijzigd, opslaan en sluiten de **wp-config.php** bestand.
   3. Gebruik de [een web-app in Azure App Service implementeren] [ deploy] informatie om de implementatiemethode die u wilt gebruiken, en vervolgens implementeert uw WordPress back-up voor uw web-app in Azure App Service.
5. Nadat de WordPress-site is geïmplementeerd, moet u kunnen toegang tot de nieuwe site (als een App Service-web-app) met de *. azurewebsite.net-URL voor de site.

### <a name="configure-your-site"></a>Uw site configureren
Nadat de WordPress-site is gemaakt of gemigreerd, gebruik de volgende informatie op de prestaties verbeteren of aanvullende functionaliteit in te schakelen.

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **App Service plan modus, grootte en schaal inschakelen instellen** |[Een web-app schalen in Azure App Service][websitescale]. |
| **Permanente databaseverbindingen inschakelen** |WordPress gebruikt standaard geen permanente databaseverbindingen, wat kunnen leiden tot de verbinding met de database na meerdere verbindingen worden beperkt. Als u permanente verbindingen installeert de [permanente verbindingen adapter invoegtoepassing](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **De prestaties verbeteren** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Uitschakelen van de cookie ARR</a>, die de prestaties kan verbeteren wanneer WordPress wordt uitgevoerd op meerdere exemplaren van de Web-Apps.</p></li><li><p>Opslaan in cache inschakelt. U kunt <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis-cache</a> (preview) met de <a href="https://wordpress.org/plugins/redis-object-cache/">Redis-cache WordPress-invoegtoepassing voor object</a>, of kunt u een van de cache in aanbiedingen van de <a href="/gallery/store/">Azure Store</a>.</p></li><li><p>[Maken van WordPress sneller met Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache is standaard ingeschakeld voor web-apps. Wanneer u WinCache en dynamische Cache samen, uitschakelen van WinCache bestandscache, maar laat de gebruiker en de sessiecache is ingeschakeld. Als u wilt uitschakelen bestandscache in een systeemniveau ini-bestand, moet u de volgende waarde instelt:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Een web-app schalen in Azure App Service] [ websitescale] en gebruik <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB hoge beschikbaarheid routering</a> of <a href="http://www.mysql.com/products/cluster/">MySQL-Cluster CGE</a>.</p></li></ul> |
| **Blobs gebruikt voor de opslag** |<ol><li><p>[Een Azure storage-account maken](../storage/common/storage-create-storage-account.md).</p></li><li><p>Meer informatie over hoe [gebruiken inhoud distributienetwerk](../cdn/cdn-create-new-endpoint.md) naar geo-gegevens die zijn opgeslagen in blobs distribueren.</p></li><li><p>Installeer en configureer de <a href="https://wordpress.org/plugins/windows-azure-storage/">Azure Storage voor WordPress-invoegtoepassing</a>.</p><p>Zie voor gedetailleerde informatie over installatie en configuratie voor de invoegtoepassing, de <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">gebruikershandleiding</a>.</p> </li></ol> |
| **E-mail inschakelen** |Schakel <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> met behulp van de Azure Store. Installeer de <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid-invoegtoepassing</a> voor WordPress. |
| **Een aangepaste domeinnaam configureren** |[Een aangepaste domeinnaam configureren in Azure App Service][customdomain]. |
| **HTTPS inschakelen voor een aangepaste domeinnaam** |[HTTPS inschakelen voor een web-app in Azure App Service][httpscustomdomain]. |
| **Laden van saldo of geo-distribueren van uw site** |[Met Azure Traffic Manager-verkeer routeren][trafficmanager]. Als u een aangepast domein gebruikt, raadpleegt u [een aangepaste domeinnaam configureren in Azure App Service] [ customdomain] voor informatie over het gebruik van Traffic Manager met aangepaste domeinnamen. |
| **Automatische back-ups inschakelen** |[Maak een back-up van een web-app in Azure App Service][backup]. |
| **Diagnostische logboekregistratie inschakelen** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service][log]. |

## <a name="next-steps"></a>Volgende stappen
* [WordPress-optimalisatie](http://codex.wordpress.org/WordPress_Optimization)
* [WordPress converteren naar meerdere locaties in Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [ClearDB wizard voor Azure bijwerken](http://www.cleardb.com/store/azure/upgrade)
* [Hosting WordPress in een submap van uw web-app in Azure App Service](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Stap voor stap: Een WordPress-site met behulp van Azure maken](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Host uw bestaande WordPress-blog op Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Permalinks in WordPress inschakelen](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Migratie en het uitvoeren van de WordPress-blog op Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Het WordPress gratis uitvoeren op Azure App Service](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress in Azure binnen twee minuten of minder](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Een WordPress-blog verplaatsen naar Azure - deel 1: een WordPress-blog op Azure maken](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Een WordPress-blog verplaatsen naar Azure - deel 2: uw Inhoudsoverdracht](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Een WordPress-blog verplaatsen naar Azure - deel 3: uw aangepaste domein instellen](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Een WordPress-blog verplaatsen naar Azure - deel 4: permalinks en regels voor het herschrijven van URL's](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Een WordPress-blog verplaatsen naar Azure - onderdeel 5: verplaatsen van een submap naar de hoofdmap](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Het instellen van een WordPress-web-app in uw Azure-account](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Propping van WordPress in Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Tips voor WordPress in Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Als u aan de slag met Azure App Service wilt voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard vereist en er bent nergens toe verplicht.
>
>

## <a name="whats-changed"></a>Wat is er gewijzigd
Zie voor een handleiding voor het wijzigen van websites in App Service, [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
