---
title: aaaCreate van hello Azure Marketplace een web-app | Microsoft Docs
description: Meer informatie over hoe een nieuwe WordPress web-app van hello Azure Marketplace met behulp van toocreate hello Azure-Portal.
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
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Een WebApp maken vanuit hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketplace biedt een breed scala aan populaire web-apps die zijn ontwikkeld door open-source software-community's, bijvoorbeeld WordPress en Umbraco CMS. In deze zelfstudie leert u hoe toocreate WordPress-app vanuit Azure marketplace.
een Azure-Web-App en MySQL-database gemaakt. 

![Voorbeeld van de WordPress-web-app dashboard](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Voordat u begint 

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="deploy-from-azure-marketplace"></a>Implementeren vanuit Azure Marketplace
Voer onderstaande toodeploy WordPress Hallo stappen uit Azure Marketplace.

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure
Meld u bij toohello [Azure-portal](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>WordPress-sjabloon implementeren
Hello Azure Marketplace bevat sjablonen voor het instellen van resources, setup Hallo [WordPress](https://portal.azure.com/#create/WordPress.WordPress) sjabloon tooget gestart.
   
Voer de volgende Hallo informatie toodeploy Hallo WordPress-app en de bijbehorende bronnen.

  ![WordPress maken stroom](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Veld         | Voorgestelde waarde           | Beschrijving  |
| ------------- |-------------------------|-------------|
| App-naam      | mywordpressapp          | Geef een unieke app-naam voor uw **Web-Appnaam**. Deze naam wordt gebruikt als onderdeel van Hallo standaard DNS-naam voor uw app `<app_name>.azurewebsites.net`, dus toobe uniek zijn in alle apps in Azure moet. U kunt later een aangepast domein naam tooyour app toewijzen voordat u deze tooyour gebruikers weergeven |
| Abonnement  | Betalen per gebruik             | Selecteer een **Abonnement**. Als u meerdere abonnementen hebt, kiest u het juiste abonnement Hallo. |
| Resourcegroep| mywordpressappgroup                 |    Voer een **resourcegroep**. Een resourcegroep is een logische container in welke Azure-resources zoals web-apps, databases die is geïmplementeerd en beheerd. U kunt een resourcegroep maken of gebruiken van een bestaande |
| App Service-plan | myappplan          | App Service-abonnementen vertegenwoordigen Hallo-verzameling van fysieke resources gebruikt toohost uw apps. Selecteer Hallo **locatie** en Hallo **prijscategorie**. Zie voor meer informatie over prijzen [App service-prijscategorie](https://azure.microsoft.com/pricing/details/app-service/) |
| Database      | mywordpressapp          | Hallo juiste databaseprovider selecteren voor MySQL. Web-Apps ondersteunt **ClearDB**, **Azure Database voor MySQL** en **MySQL in-app**. Zie voor meer informatie [databaseconfiguratie](#database-config) hieronder. |
| Application Insights | ON of OFF          | Dit is optioneel. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) bewakingsservices voor uw web-app biedt door te klikken op **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Databaseconfiguratie
Volgende stappen uit Hallo op basis van uw keuze van MySQL-database-provider.  Het verdient aanbeveling die zowel Web-App en MySQL-database zich op Hallo dezelfde locatie.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) is een oplossing van derden voor een volledig geïntegreerde MySQL-service op Azure. In de volgorde toouse ClearDB databases, moet u een creditcard tooyour tooassociate [Azure-account](http://account.windowsazure.com/subscriptions). Als u ClearDB databaseprovider hebt geselecteerd, kunt u een lijst met bestaande databases toochoose van weergeven of klik op **nieuw** knop toocreate een database.

![ClearDB maken](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Azure-Database voor MySQL (Preview)
[Azure MySQL-Database](https://azure.microsoft.com/en-us/services/mysql) is een beheerde databaseservice voor app-ontwikkeling en implementatie waarmee u toostand van een MySQL-database in minuten en schaal op Hallo vliegen op Hallo cloud u meest vertrouwt. Met liggen prijscategorie modellen, beschikt u over alle mogelijkheden van Hallo zoals hoge beschikbaarheid, beveiliging en herstel gewenste – ingebouwd, zonder extra kosten. Klik op **prijscategorie** toochoose een andere [prijscategorie](https://azure.microsoft.com/pricing/details/mysql). toouse een bestaande database of bestaande MySQL-server, gebruikt u een bestaande resourcegroep in welke Hallo-server zich bevindt. 

![Database-instellingen voor web-app Hallo Hallo configureren](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure-Database voor MySQL (Preview) en Web-App op Linux (Preview) zijn niet beschikbaar in alle regio's. meer informatie over toolearn [Azure Database voor MySQL (Preview)](https://docs.microsoft.com/en-us/azure/mysql) en [Web-App op Linux](./app-service-linux-intro.md) beperkingen. 

#### <a name="mysql-in-app"></a>MySQL in-app
[MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) is een functie van App-Service waarmee MySql systeemeigen uitgevoerd op Hallo-platform. Hallo Kernfunctionaliteit Hallo-versie van de functie Hallo ondersteund:

- MySQL-server op Hallo dezelfde naast uw webserver die als host fungeert voor de site Hallo-instantie. Dit verhoogt de prestaties van uw toepassing.
- Opslag wordt gedeeld tussen de MySQL- en uw web-app-bestanden. Houd er rekening mee met vrije en gedeelde plannen die u mogelijk op onze quotalimieten wanneer Hallo site gebruiken op basis van Hallo acties u uitvoeren. Bekijk [quotumbeperkingen](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) voor vrije en gedeelde plannen.
- U kunt trage queryregistratie en algemene logboekregistratie in voor MySQL inschakelt. Houd er rekening mee dat dit invloed op prestaties van de site Hallo hebben kan en moet niet altijd ingeschakeld. Hallo logboekregistratie functie helpt bij het onderzoeken van toepassingsproblemen. 

Voor meer informatie, Bekijk dit [artikel](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![MySQL appbeheer](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

U kunt de voortgang Hallo bekijken door te klikken op het belpictogram Hallo Hallo boven aan de portalpagina Hallo tijdens het Hallo WordPress-app wordt geïmplementeerd.    
![Voortgangsindicator](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Uw nieuwe Azure-web-app beheren

Ga toohello Azure portal tootake bekijkt hello web-app die u zojuist hebt gemaakt.

toodo dit te melden[https://portal.azure.com](https://portal.azure.com).

In het linkermenu hello, klikt u op **App Services**, klikt u op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


U bent aangekomen op de _blade_ van uw web-app (een portalpagina die horizontaal wordt geopend).

Standaard ziet u uw web-app-blade Hallo **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. Hallo tabbladen aan de linkerkant Hallo van Hallo blade ziet Hallo verschillende configuratiepagina's die u kunt openen.

![App Service-blade in Azure Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Deze tabbladen Hallo blade bevatten Hallo vele handige functies u tooyour web-app kunt toevoegen. Hallo na lijst hebt u slechts een paar van Hallo mogelijkheden:

* Een aangepaste DNS-naam toewijzen
* Een aangepast SSL-certificaat binden
* Continue implementatie inschakelen
* Omhoog en omlaag schalen
* Gebruikersverificatie toevoegen

Hallo 5 minuten WordPress installatie wizard toohave WordPress-app snel voltooien. Bekijk [Wordpress documentatie](https://codex.WordPress.org/) toodevelop uw web-app.

![WordPress-installatiewizard](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configureren van de app 
Er zijn meerdere stappen die betrokken zijn bij het beheren van uw WordPress-app voordat deze gereed voor gebruik in productieomgevingen is. Volg deze stappen tooconfigure en beheren van uw WordPress-app:

| toodo dit... | Gebruikt u... |
| --- | --- |
| **Uploaden of opslaan van grote bestanden** |[WordPress-invoegtoepassing voor het gebruik van Blob-opslag](https://wordpress.org/plugins/windows-azure-storage/)|
| **E-mail verzenden** |Aankoop [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) e-service en gebruik Hallo [WordPress-invoegtoepassing voor het gebruik van SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure deze|
| **Aangepaste domeinnamen** |[Een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[HTTPS inschakelen voor een web-app in Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Validatie van vóór productie** |[Faserings- en Developer omgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)|
| **Bewaking en probleemoplossing** |[Logboekregistratie van diagnostische gegevens van web-apps in Azure App Service](web-sites-enable-diagnostic-log.md) en [Web-Apps bewaken in Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Uw site implementeren** |[Een web-app in Azure App Service implementeren](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Beveiligen van uw app 
Er zijn meerdere stappen die betrokken zijn bij het beheren van uw WordPress-app voordat deze gereed voor gebruik in productieomgevingen is. Volg deze stappen tooconfigure en beheren van uw WordPress-app:

| toodo dit... | Gebruikt u... |
| --- | --- |
| **Sterke gebruikersnaam en wachtwoord**|  Wachtwoord regelmatig wordt gewijzigd. Kan geen gebruik gebruikte gebruikersnamen, zoals *admin* of *wordpress* enzovoort. Alle WordPress gebruikers toouse unieke gebruikersnaam en sterke wachtwoorden te forceren. |
| **De hoogte blijven** | Houd uw WordPress-core, thema's, invoegtoepassingen up toodate. Hallo nieuwste PHP-runtime beschikbaar is in Azure App service gebruiken |
| **WordPress-beveiligingssleutels bijwerken** | Update [WordPress beveiligingssleutel](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tooimprove versleuteling is opgeslagen in cookies|

## <a name="improve-performance"></a>De prestaties verbeteren
Prestaties in de cloud Hallo wordt hoofdzakelijk door opslaan in cache en scale-out bereikt. Hallo-geheugen, bandbreedte en andere kenmerken van het hosten van Web-Apps moeten echter wel beschouwd als.

| toodo dit... | Gebruikt u... |
| --- | --- |
| **De mogelijkheden van App Service-exemplaar begrijpen** |[Prijsinformatie, met inbegrip van de mogelijkheden van App Service-lagen](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Cache-resources** |Gebruik [Azure Redis-cache](https://azure.microsoft.com/en-us/services/cache/), of een van andere cachebewerkingen aanbiedingen voor Hallo Hallo [Azure Store](https://azuremarketplace.microsoft.com) |
| **Uw toepassing schalen** |U moet tooscale [Hallo web-app in Azure App Service](web-sites-scale.md) en/of een MySQL-database. MySQL in-app geen ondersteuning voor scale-out, kiest daarom ClearDB of Azure Database voor MySQL (Preview). [Azure-database schalen voor MySQL (Preview)](https://azure.microsoft.com/en-us/pricing/details/mysql/) of als [ClearDB hoge beschikbaarheid routering](http://w2.cleardb.net/faqs/) tooscale van uw database |

## <a name="availability-and-disaster-recovery"></a>Beschikbaarheid en herstel na noodgevallen
Hoge beschikbaarheid omvat Hallo aspect van disaster recovery toomaintain zakelijke continuïteit. Planning voor de fouten en noodsituaties in de cloud hello, moet u toorecognize Hallo fouten snel. Deze oplossingen helpen bij het implementeren van een strategie voor maximale beschikbaarheid.

| toodo dit... | Gebruikt u... |
| --- | --- |
| **Laden van saldo sites** of **geo-sites distribueren** |[Verkeer leiden met Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Back-ups maken en bestanden terugzetten** |[Maak een back-up van een web-app in Azure App Service](web-sites-backup.md) en [herstellen van een web-app in Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over de verschillende functies van [toodevelop App Service en de schaal](/app-service-web/).
