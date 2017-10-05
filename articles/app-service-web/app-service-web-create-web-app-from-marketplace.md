---
title: Een web-app maken vanuit Azure Marketplace | Microsoft Docs
description: Lees hoe u vanuit Azure Marketplace een nieuwe WordPress-web-app maakt met behulp van de Azure Portal.
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 16951ac0fcc350b7176747a7ad4e0bc8e186ab17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-from-the-azure-marketplace"></a>Een web-app maken vanuit Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Azure Marketplace biedt een breed scala aan populaire web-apps die zijn ontwikkeld door open-source software-community's, bijvoorbeeld WordPress en Umbraco CMS. In deze zelfstudie leert u hoe WordPress-app maken vanuit Azure marketplace.
een Azure-Web-App en MySQL-database gemaakt. 

![Voorbeeld van de WordPress-web-app dashboard](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Voordat u begint 

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="deploy-from-azure-marketplace"></a>Implementeren vanuit Azure Marketplace
Volg onderstaande stappen voor het implementeren van WordPress in Azure Marketplace.

### <a name="sign-in-to-azure"></a>Aanmelden bij Azure
Meld u aan bij [Azure Portal](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>WordPress-sjabloon implementeren
Azure Marketplace bevat sjablonen voor het instellen van resources, instellen van de [WordPress](https://portal.azure.com/#create/WordPress.WordPress) sjabloon aan de slag.
   
Voer de volgende informatie om de WordPress-app en de daarbij behorende bronnen te implementeren.

  ![WordPress maken stroom](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Veld         | Voorgestelde waarde           | Beschrijving  |
| ------------- |-------------------------|-------------|
| App-naam      | mywordpressapp          | Geef een unieke app-naam voor uw **Web-Appnaam**. Deze naam wordt gebruikt als onderdeel van de standaard DNS-naam voor uw app `<app_name>.azurewebsites.net`, zodat het moet uniek zijn in alle apps in Azure. U kunt later een aangepaste domeinnaam toewijzen aan uw app voordat u het beschikbaar aan uw gebruikers stellen |
| Abonnement  | Betalen per gebruik             | Selecteer een **Abonnement**. Als u meerdere abonnementen hebt, kiest u het juiste abonnement. |
| Resourcegroep| mywordpressappgroup                 |    Voer een **resourcegroep**. Een resourcegroep is een logische container in welke Azure-resources zoals web-apps, databases die is geïmplementeerd en beheerd. U kunt een resourcegroep maken of gebruiken van een bestaande |
| App Service-plan | myappplan          | App Service-abonnementen staan voor de verzameling van fysieke resources die worden gebruikt voor het hosten van uw apps. Selecteer de **locatie** en de **prijscategorie**. Zie voor meer informatie over prijzen [App service-prijscategorie](https://azure.microsoft.com/pricing/details/app-service/) |
| Database      | mywordpressapp          | Selecteer de juiste database-provider voor MySQL. Web-Apps ondersteunt **ClearDB**, **Azure Database voor MySQL** en **MySQL in-app**. Zie voor meer informatie [databaseconfiguratie](#database-config) hieronder. |
| Application Insights | ON of OFF          | Dit is optioneel. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) bewakingsservices voor uw web-app biedt door te klikken op **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Databaseconfiguratie
Volg de stappen op basis van uw keuze van MySQL-database-provider.  Het is raadzaam dat die zowel Web-App en MySQL-database zich op dezelfde locatie bevinden.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) is een oplossing van derden voor een volledig geïntegreerde MySQL-service op Azure. Als u wilt gebruiken ClearDB databases, moet u een creditcard koppelen uw [Azure-account](http://account.windowsazure.com/subscriptions). Als u ClearDB databaseprovider hebt geselecteerd, kunt u een lijst met bestaande databases te kiezen uit of klik op bekijken **nieuw** knop om een database te maken.

![ClearDB maken](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Azure-Database voor MySQL (Preview)
[Azure MySQL-Database](https://azure.microsoft.com/en-us/services/mysql) is een beheerde databaseservice voor app-ontwikkeling en implementatie waarmee u een MySQL-database in minuten voldoen en schalen op elk gewenst moment in de cloud de meeste vertrouwt. Met liggen prijscategorie modellen, beschikt u over alle mogelijkheden van de gewenste zoals hoge beschikbaarheid, beveiliging en herstel – ingebouwd, zonder extra kosten. Klik op **prijscategorie** kiezen een andere [prijscategorie](https://azure.microsoft.com/pricing/details/mysql). U kunt een bestaande database of een bestaande MySQL-server, gebruiken een bestaande resourcegroep waarin de server zich bevindt. 

![De database-instellingen voor de web-app configureren](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure-Database voor MySQL (Preview) en Web-App op Linux (Preview) zijn niet beschikbaar in alle regio's. Voor meer informatie over [Azure Database voor MySQL (Preview)](https://docs.microsoft.com/en-us/azure/mysql) en [Web-App op Linux](./app-service-linux-intro.md) beperkingen. 

#### <a name="mysql-in-app"></a>MySQL in-app
[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) is een functie van App-Service waarmee MySql systeemeigen uitgevoerd op het platform. De kernfunctionaliteit ondersteund met de release van de functie:

- MySQL-server met hetzelfde exemplaar naast elkaar met de webserver die als host fungeert voor de site. Dit verhoogt de prestaties van uw toepassing.
- Opslag wordt gedeeld tussen de MySQL- en uw web-app-bestanden. Houd er rekening mee met vrije en gedeelde plannen die u mogelijk op onze quotalimieten wanneer met behulp van de site op basis van de acties die u uitvoert. Bekijk [quotumbeperkingen](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) voor vrije en gedeelde plannen.
- U kunt trage queryregistratie en algemene logboekregistratie in voor MySQL inschakelt. Houd er rekening mee dat dit invloed op de prestaties van de site hebben kan en moet niet altijd ingeschakeld. De functie voor logboekregistratie kunt onderzoeken van toepassingsproblemen. 

Voor meer informatie, Bekijk dit [artikel](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![MySQL appbeheer](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

U kunt de voortgang bekijken door te klikken op het belpictogram boven aan de portal-pagina, terwijl de WordPress-app wordt geïmplementeerd.    
![Voortgangsindicator](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Uw nieuwe Azure-web-app beheren

Ga naar Azure Portal om de web-app die u zojuist hebt gemaakt, te bekijken.

Hiervoor moet u zich aanmelden bij [https://portal.azure.com](https://portal.azure.com).

Klik vanuit het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


U bent aangekomen op de _blade_ van uw web-app (een portalpagina die horizontaal wordt geopend).

Standaard toont de blade van uw web-app de pagina **Overzicht**. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. De tabbladen aan de linkerkant van de blade tonen de verschillende configuratiepagina's die u kunt openen.

![App Service-blade in Azure Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Deze tabbladen op de blade bevatten de vele handige functies die kunt u toevoegen aan uw web-app. De volgende lijst bevat slechts enkele van de mogelijkheden:

* Een aangepaste DNS-naam toewijzen
* Een aangepast SSL-certificaat binden
* Continue implementatie inschakelen
* Omhoog en omlaag schalen
* Gebruikersverificatie toevoegen

Voltooi de installatiewizard voor WordPress van 5 minuten als u wilt dat de WordPress-app zetten. Bekijk [Wordpress documentatie](https://codex.WordPress.org/) voor het ontwikkelen van uw web-app.

![WordPress-installatiewizard](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configureren van de app 
Er zijn meerdere stappen die betrokken zijn bij het beheren van uw WordPress-app voordat deze gereed voor gebruik in productieomgevingen is. Volg deze stappen voor het configureren en beheren van uw WordPress-app:

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **Uploaden of opslaan van grote bestanden** |[WordPress-invoegtoepassing voor het gebruik van Blob-opslag](https://wordpress.org/plugins/windows-azure-storage/)|
| **E-mail verzenden** |Aankoop [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) e-service en gebruik de [WordPress-invoegtoepassing voor het gebruik van SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) configureren|
| **Aangepaste domeinnamen** |[Een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[HTTPS inschakelen voor een web-app in Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Validatie van vóór productie** |[Faserings- en Developer omgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)|
| **Bewaking en probleemoplossing** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](web-sites-enable-diagnostic-log.md) en [Web-Apps bewaken in Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Uw site implementeren** |[Een web-app in Azure App Service implementeren](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Beveiligen van uw app 
Er zijn meerdere stappen die betrokken zijn bij het beheren van uw WordPress-app voordat deze gereed voor gebruik in productieomgevingen is. Volg deze stappen voor het configureren en beheren van uw WordPress-app:

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **Sterke gebruikersnaam en wachtwoord**|  Wachtwoord regelmatig wordt gewijzigd. Kan geen gebruik gebruikte gebruikersnamen, zoals *admin* of *wordpress* enzovoort. Afdwingen dat alle gebruikers van WordPress unieke gebruikersnaam en sterke wachtwoorden gebruiken. |
| **De hoogte blijven** | Uw WordPress-core, thema's, invoegtoepassingen up-to-date te houden. Gebruik de meest recente PHP-runtime beschikbaar is in Azure App service |
| **WordPress-beveiligingssleutels bijwerken** | Update [WordPress beveiligingssleutel](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) voor het verbeteren van de versleuteling is opgeslagen in cookies|

## <a name="improve-performance"></a>De prestaties verbeteren
Prestaties in de cloud wordt bewerkstelligd voornamelijk met caching en scale-out. Echter, moeten het geheugen, bandbreedte en andere kenmerken van het hosten van Web-Apps worden beschouwd.

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **De mogelijkheden van App Service-exemplaar begrijpen** |[Prijsinformatie, met inbegrip van de mogelijkheden van App Service-lagen](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Cache-resources** |Gebruik [Azure Redis-cache](https://azure.microsoft.com/en-us/services/cache/), of een van de cache in aanbiedingen in de [Azure Store](https://azuremarketplace.microsoft.com) |
| **Uw toepassing schalen** |U hoeft te schalen [de web-app in Azure App Service](web-sites-scale.md) en/of een MySQL-database. MySQL in-app geen ondersteuning voor scale-out, kiest daarom ClearDB of Azure Database voor MySQL (Preview). [Azure-database schalen voor MySQL (Preview)](https://azure.microsoft.com/en-us/pricing/details/mysql/) of als [ClearDB hoge beschikbaarheid routering](http://w2.cleardb.net/faqs/) schalen van uw database |

## <a name="availability-and-disaster-recovery"></a>Beschikbaarheid en herstel na noodgevallen
Hoge beschikbaarheid omvat het aspect van herstel na noodgevallen voor het onderhouden van zakelijke continuïteit. Planning voor de fouten en noodsituaties in de cloud, moet u de fouten snel herkennen. Deze oplossingen helpen bij het implementeren van een strategie voor maximale beschikbaarheid.

| Als u dit wilt doen... | Gebruikt u... |
| --- | --- |
| **Laden van saldo sites** of **geo-sites distribueren** |[Verkeer leiden met Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Back-ups maken en bestanden terugzetten** |[Maak een back-up van een web-app in Azure App Service](web-sites-backup.md) en [herstellen van een web-app in Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over de verschillende functies van [App Service te ontwikkelen en schalen](/app-service-web/).