---
title: aaaCreate en verbinding maken met tooa MySQL-database in Azure
description: Ontdek hoe toouse hello Azure portal toocreate een MySQL-database en vervolgens verbinding tooit van een PHP-web-app in Azure.
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Maken en verbinding maken met tooa MySQL-database in Azure
Deze zelfstudie laat zien hoe toocreate een MySQL-database in Hallo [Azure-portal](https://portal.azure.com) (provider [ClearDB](http://www.cleardb.com/)) en hoe tooconnect tooit van een PHP web-app uitgevoerd in de [Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> U kunt ook een MySQL-database maken als onderdeel van een [Marketplace-app-sjabloon](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Een MySQL-database maken in Azure portal
een MySQL-database in Azure-portal Hallo toocreate Hallo te volgen:

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. In het linkermenu hello, klikt u op **nieuw** > **gegevens en opslag** > **MySQL-Database**.

    ![Een MySQL-database maken in Azure - starten](./media/store-php-create-mysql-database/create-db-1-start.png)
3. In de nieuwe MySQL-Database Hallo [blade](azure-portal-overview.md), als volgt uw nieuwe MySQL-database configureren (*blade*: een portal-pagina dat wordt geopend horizontaal):

   * **Databasenaam**: Typ een naam uniek identificeerbaar
   * **Abonnement**: Hallo abonnement toouse kiezen
   * **Type van de database**: Selecteer **gedeelde** voor lage kosten of gratis lagen, of **toegewezen** tooget toegewezen resources.
   * **Resourcegroep**: Hallo MySQL database tooan bestaande toevoegen [resourcegroep](azure-resource-manager/resource-group-overview.md) of in een nieuwe plaatsen. Bronnen in dezelfde groep kan eenvoudig worden beheerd samen Hallo.
   * **Locatie**: Selecteer een locatie sluiten tooyou. Wanneer u bestaande resourcegroep tooan toevoegt, bent u vergrendelde toohello-resourcegroep van locatie.
   * **Prijscategorie**: klik op **prijscategorie**, selecteert u vervolgens een optie prijscategorie (**Mercury** is de laag gratis), en klik vervolgens op **selecteren**.
   * **Juridische voorwaarden**: klik op **juridische voorwaarden**bekijkt hello inkoopgegevens, en op **kopen**.
   * **Pincode toodashboard**: Selecteer deze optie als u wilt dat tooaccess rechtstreeks vanuit het Hallo-dashboard. Dit is vooral handig als u niet bekend bent met de navigatie in de portal nog.

     Hallo volgende schermafbeelding is slechts een voorbeeld van hoe u uw MySQL-database kunt configureren.  
     ![Een MySQL-database maken in Azure - configureren](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Wanneer u klaar bent configureren, klikt u op **maken**.

    ![Een MySQL-database maken in Azure - maken](./media/store-php-create-mysql-database/create-db-3-create.png)

    Hier ziet u een pop-upbericht waarin wordt aangegeven dat de implementatie is gestart.

    ![Maken van een MySQL-database in Azure - uitgevoerd](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Krijgt u een andere pop-up zodra de implementatie is geslaagd. Hallo-portal wordt de blade van uw MySQL-database ook automatisch geopend.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Verbinding maken met tooyour MySQL-database
toosee Hallo-verbindingsgegevens voor de nieuwe MySQL-database, klikt u op **eigenschappen** in uw web-app-blade.

![Een MySQL-database maken in Azure - blade MySQL-database](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

U kunt nu verbindingsinformatie in een web-app. Een steekproef die wordt weergegeven hoe toouse Hallo-verbindingsinformatie van een eenvoudige PHP-app beschikbaar is [hier](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Verbinding maken met een Laravel web-app (uit Hallo PHP get gestart zelfstudie)
Stel dat u net klaar Hallo zelfstudie [maken, configureren en implementeren van een PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) en hebben een [Laravel](https://www.laravel.com/) web-app in Azure wordt uitgevoerd. U kunt eenvoudig database mogelijkheden tooyour Laravel app toevoegen. Volg onderstaande stappen voor Hallo:

> [!NOTE]
> Hallo volgende stappen wordt ervan uitgegaan dat u klaar bent met het Hallo-zelfstudie [maken, configureren en implementeren van een PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).
>
>

1. Hallo Laravel app configureren in uw lokale ontwikkeling omgeving toopoint toohello MySQL-database. toodo deze, open `.env` de hoofdmap van uw Laravel-app en Hallo MySQL-database-opties configureren.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > In Hallo **eigenschappen** blade Hallo-naam van uw MySQL-database mogelijk of worden mogelijk niet Hallo een weergegeven in Hallo **DATABASENAAM** veld. Het is beter toocheck hello databaseparameter in Hallo **VERBINDINGSREEKS** veld.    
   >
   > ![Maken van een MySQL-database in Azure - uitgevoerd](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Hallo snelste manier tooverify dat u gemachtigd MySQL nu is toouse [Laravel van standaard verificatie steigers](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Uitvoeren in Hallo opdrachtregelprogramma terminal Hallo volgende opdrachten uit de hoofdmap van uw app Laravel:

         php artisan migrate
         php artisan make:auth

    de eerste opdracht Hallo Hallo tabellen gemaakt in Azure op basis van vooraf gedefinieerde migraties in Hallo `database/migrations` directory en de tweede opdracht Hallo platforms Hallo basic weergaven en routes voor gebruikersregistratie en verificatie.
3. Hallo-ontwikkelaarsserver nu uitvoeren:

        php artisan serve
4. Navigeer toohttp://localhost:8000 in Hallo browser en een nieuwe gebruiker registreren, zoals wordt weergegeven:

    ![Verbinding maken met tooMySQL database in Azure - registreren van de gebruiker](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Ga als volgt Hallo UI vragen voltooid Hallo registratie. Wanneer de registratie is voltooid, wordt u vastgelegd in.

    ![Verbinding maken met tooMySQL database in Azure - registreren van de gebruiker](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    U nu ontwikkelt uw app op Hallo MySQL-database in Azure.
5. Nu hoeft u alleen tooreplicate uw `.env` instellingen tooyour Azure-web-app. Voer hello Azure CLI-opdrachten te volgen:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Vervolgens doorvoeren en push tooAzure Hallo lokale wijzigingen eerder tijdens de uitvoering `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Blader toohello Azure-web-app.

        azure site browse
8. Meld u aan met de Hallo-gebruikersreferenties die u eerder hebt gemaakt.

    ![Verbinding maken met tooMySQL database in Azure - web-app tooAzure bladeren](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Nadat u zich hebt aangemeld, ziet u beschrijvende na de aanmelding welkomstscherm.

    ![Verbinding maken met tooMySQL database in Azure - aangemeld](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Gefeliciteerd, uw PHP-web-app in Azure is nu toegang tot gegevens uit uw MySQL-database.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).
