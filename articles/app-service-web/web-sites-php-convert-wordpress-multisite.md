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
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a>WordPress converteren naar meerdere locaties in Azure App Service
## <a name="overview"></a>Overzicht
*Door [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

In deze zelfstudie leert u een bestaande web-app voor WordPress is gemaakt door de galerie in Azure maken en deze omzetten in een implementatie voor meerdere locaties WordPress-installatie. Bovendien leert u hoe u een aangepast domein toewijzen aan elk van de subsites binnen uw installatie.

Ervan wordt uitgegaan dat u een bestaande installatie van WordPress hebt. Volg de richtlijnen als u dit niet doet, [een WordPress-website maken vanuit de Azure-galerie][website-from-gallery].

Converteren van een bestaande WordPress één site installeren op meerdere locaties is doorgaans redelijk eenvoudig en veel van de eerste stappen die hier worden geleverd rechtstreeks vanuit de [maken van een netwerk] [ wordpress-codex-create-a-network] pagina op de [ WordPress Codex](http://codex.wordpress.org).

Aan de slag.

## <a name="allow-multisite"></a>Implementatie voor meerdere locaties toestaan
U moet eerst meerdere locaties via inschakelen de `wp-config.php` het bestand met de **WP\_toestaan\_implementatie voor meerdere locaties** constante. Er zijn twee methoden voor het bewerken van uw web-app-bestanden: de eerste is via de FTP- en de tweede via Git. Als u niet bekend met het instellen van deze methoden bent, raadpleegt u de volgende zelfstudies:

* [PHP-website met de MySQL- en FTP-][website-w-mysql-and-ftp-ftp-setup]
* [PHP-website met de MySQL en Git][website-w-mysql-and-git-git-setup]

Open de `wp-config.php` -bestand met een editor van uw keuze en voeg de volgende bovenstaande de `/* That's all, stop editing! Happy blogging. */` regel.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Zorg dat het bestand opslaan en upload het naar de server!

## <a name="network-setup"></a>Netwerk instellen
Meld u aan bij de *wp-beheerder* ruimte van uw web-app en u ziet een nieuw item onder de **extra** menu aangeroepen **netwerkinstellingen**. Klik op **netwerkinstellingen** en vult u de details van uw netwerk.

![Scherm voor het netwerk instellen][wordpress-network-setup]

Deze zelfstudie wordt gebruikgemaakt van de *submappen* schema site omdat deze altijd werkt en we om de aangepaste domeinen van de bovenliggende verderop in de zelfstudie instellen. Echter, moet het mogelijk installatie van een subdomein installeren als u een domein via toewijzen voor de [Azure Portal](https://portal.azure.com) en jokerteken DNS correct setup.

Zie voor meer informatie over het subdomein tegenover submap instellingen de [soorten multisiteconfiguratie] [ wordpress-codex-types-of-networks] artikel op de WordPress-Codex.

## <a name="enable-the-network"></a>Het netwerk inschakelen
Het netwerk is nu geconfigureerd in de database, maar er is een resterende stap in het inschakelen van de netwerkfunctionaliteit. Voltooi de `wp-config.php` instellingen en zorg ervoor dat `web.config` goed routeert elke site.

Wanneer u op de **installeren** knop op de *netwerkinstellingen* pagina WordPress probeert bij te werken de `wp-config.php` en `web.config` bestanden. U moet echter altijd de bestanden om te controleren of dat de updates met succes zijn controleren. Als dit niet het geval is, wordt dit scherm u met de vereiste updates worden geïnstalleerd. Bewerken en opslaan van de bestanden.

Nadat u back deze updates u moet af en meld in het dashboard wp-beheerder.

Er worden nu een menu Extra op de admin-balk met het label **Mijn Sites**. Dit menu kunt u bepalen van uw nieuwe netwerk via de **netwerk Admin** dashboard.

## <a name="adding-custom-domains"></a>Toevoegen van aangepaste domeinen
De [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] invoegtoepassing kunt u probleemloos aangepaste domeinen toevoegen aan een site in uw netwerk. Voor de invoegtoepassing correcte werking moet, u enkele aanvullende instellingen op de Portal en bij uw domeinregistrar doen.

## <a name="enable-domain-mapping-to-the-web-app"></a>Domein toewijzen aan de web-app
De **vrije** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan modus biedt geen ondersteuning voor het toevoegen van aangepaste domeinen aan Web-Apps. U moet overschakelen naar **gedeelde** of **standaard** modus. Om dit te doen:

* Aanmelden bij de Azure-Portal en zoek uw web-app. 
* Klik op de **opschalen** tabblad **instellingen**.
* Onder **algemene**, selecteert u *gedeelde* of *STANDARD*
* Klik op **opslaan**

U wordt gevraagd om te controleren of de wijziging en bevestigt dat uw web-app kan nu kosten in rekening gebracht een, al naar gelang het verbruik en de andere configuratie die u instelt.

Het duurt een paar seconden voor het verwerken van de nieuwe instellingen is nu een goed moment om het instellen van uw domein te starten.

## <a name="verify-your-domain"></a>Verifieer uw domein
Voordat u Azure Web Apps kunt u een domein worden toegewezen aan de site, moet u eerst controleren of u de autorisatie hebt voor het toewijzen van het domein. Om dit te doen, moet u een nieuwe CNAME-record toevoegen aan uw DNS-vermelding.

* Aanmelden bij uw domein-DNS-beheer
* Maakt een nieuwe CNAME *awverify*
* Punt *awverify* naar *awverify. YOUR_DOMAIN.azurewebsites.NET*

Het kan even duren voordat de DNS-wijzigingen van kracht volledige, dus als u de volgende stappen werken niet onmiddellijk gaat koffie, maken en vervolgens keert u terug en probeer het opnieuw.

## <a name="add-the-domain-to-the-web-app"></a>Het domein toevoegen aan de web-app
Ga terug naar uw web-app via de Azure-Portal, klikt u op **instellingen**, en klik vervolgens op **aangepaste domeinen en SSL**.

Wanneer de *SSL-instellingen* worden weergegeven, ziet u de velden waar u invoer op alle domeinen die u wilt toewijzen aan uw web-app. Als een domein is hier niet worden vermeld, is het niet mogelijk voor de toewijzing binnen WordPress, ongeacht hoe de domein-DNS ingesteld is.

![Dialoogvenster aangepaste domeinen beheren][wordpress-manage-domains]

Nadat u uw domein in het tekstvak te typen, Azure controleert of de CNAME-record dat u eerder hebt gemaakt. Als de DNS-server is niet volledig is doorgegeven, wordt een rode indicator wordt weergegeven. Als deze voltooid is, ziet u een groen vinkje. 

Let op het IP-adres aan de onderkant van het dialoogvenster. U moet dit voor het instellen van de A-record voor uw domein.

## <a name="setup-the-domain-a-record"></a>Instellen van het domein een record
Als de andere stappen voltooid zijn, kunt u kunt nu het domein toewijzen aan uw Azure-web-app in een DNS A-record. 

Het is belangrijk te weten hier die Azure-web-apps worden geaccepteerd CNAME zowel A-records, maar u *moet* gebruikmaken van een A-record voor de toewijzing van het juiste domein. Een CNAME kan niet worden doorgestuurd naar een andere CNAME, dit is wat Azure met YOUR_DOMAIN.azurewebsites.net voor u gemaakt.

Met behulp van het IP-adres van de vorige stap, terug naar uw DNS-beheer en de A-record wijst u aan dat IP-adres instellen.

## <a name="install-and-setup-the-plugin"></a>Installeren en instellen van de invoegtoepassing
Implementatie voor meerdere locaties WordPress heeft momenteel geen ingebouwde methode om toe te wijzen van aangepaste domeinen. Er is echter een invoegtoepassing aangeroepen [WordPress MU domein toewijzing] [ wordpress-plugin-wordpress-mu-domain-mapping] waarmee de functionaliteit voor u worden toegevoegd. Aanmelden bij het netwerk Admin-gedeelte van uw site en installeer de **WordPress MU domein toewijzing** invoegtoepassing.

Na het installeren en activeren van de invoegtoepassing, gaat u naar **instellingen** > **domein toewijzing** voor het configureren van de invoegtoepassing. In het eerste tekstvak *IP-adres*, voer het IP-adres dat u gebruikt voor het instellen van de A-record voor het domein. Stel een *Domeinopties* u desire (de standaardwaarden zijn vaak fijn) en klik op **opslaan**.

## <a name="map-the-domain"></a>Het domein toewijzen
Ga naar de **Dashboard** voor de site die u wilt toewijzen van het domein. Klik op **extra** > **domein toewijzing** en typt u het nieuwe domein in het tekstvak en klik op **toevoegen**.

Standaard wordt het nieuwe domein worden herschreven aan het domein van de site automatisch gegenereerd. Als u wilt dat alle verkeer dat wordt verzonden naar het nieuwe domein, Controleer de *primair domein voor deze blog* vak voordat u opslaat. U kunt een onbeperkt aantal domeinen toevoegen aan een site, maar slechts één primaire kan zijn.

## <a name="do-it-again"></a>Opnieuw doen
Azure-Web-Apps kunt u een onbeperkt aantal domeinen toevoegen aan een web-app. Toevoegen van een ander domein, moet u uitvoeren van de **Verifieer uw domein** en **instellen van het domein een record** secties voor elk domein.    

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

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


