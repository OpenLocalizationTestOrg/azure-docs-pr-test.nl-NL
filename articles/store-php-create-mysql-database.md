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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="071b5-103">Maken en verbinding maken met tooa MySQL-database in Azure</span><span class="sxs-lookup"><span data-stu-id="071b5-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="071b5-104">Deze zelfstudie laat zien hoe toocreate een MySQL-database in Hallo [Azure-portal](https://portal.azure.com) (provider [ClearDB](http://www.cleardb.com/)) en hoe tooconnect tooit van een PHP web-app uitgevoerd in de [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="071b5-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="071b5-105">U kunt ook een MySQL-database maken als onderdeel van een [Marketplace-app-sjabloon](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="071b5-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="071b5-106">Een MySQL-database maken in Azure portal</span><span class="sxs-lookup"><span data-stu-id="071b5-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="071b5-107">een MySQL-database in Azure-portal Hallo toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="071b5-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="071b5-108">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="071b5-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="071b5-109">In het linkermenu hello, klikt u op **nieuw** > **gegevens en opslag** > **MySQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="071b5-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Een MySQL-database maken in Azure - starten](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="071b5-111">In de nieuwe MySQL-Database Hallo [blade](azure-portal-overview.md), als volgt uw nieuwe MySQL-database configureren (*blade*: een portal-pagina dat wordt geopend horizontaal):</span><span class="sxs-lookup"><span data-stu-id="071b5-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="071b5-112">**Databasenaam**: Typ een naam uniek identificeerbaar</span><span class="sxs-lookup"><span data-stu-id="071b5-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="071b5-113">**Abonnement**: Hallo abonnement toouse kiezen</span><span class="sxs-lookup"><span data-stu-id="071b5-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="071b5-114">**Type van de database**: Selecteer **gedeelde** voor lage kosten of gratis lagen, of **toegewezen** tooget toegewezen resources.</span><span class="sxs-lookup"><span data-stu-id="071b5-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="071b5-115">**Resourcegroep**: Hallo MySQL database tooan bestaande toevoegen [resourcegroep](azure-resource-manager/resource-group-overview.md) of in een nieuwe plaatsen.</span><span class="sxs-lookup"><span data-stu-id="071b5-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="071b5-116">Bronnen in dezelfde groep kan eenvoudig worden beheerd samen Hallo.</span><span class="sxs-lookup"><span data-stu-id="071b5-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="071b5-117">**Locatie**: Selecteer een locatie sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="071b5-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="071b5-118">Wanneer u bestaande resourcegroep tooan toevoegt, bent u vergrendelde toohello-resourcegroep van locatie.</span><span class="sxs-lookup"><span data-stu-id="071b5-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="071b5-119">**Prijscategorie**: klik op **prijscategorie**, selecteert u vervolgens een optie prijscategorie (**Mercury** is de laag gratis), en klik vervolgens op **selecteren**.</span><span class="sxs-lookup"><span data-stu-id="071b5-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="071b5-120">**Juridische voorwaarden**: klik op **juridische voorwaarden**bekijkt hello inkoopgegevens, en op **kopen**.</span><span class="sxs-lookup"><span data-stu-id="071b5-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="071b5-121">**Pincode toodashboard**: Selecteer deze optie als u wilt dat tooaccess rechtstreeks vanuit het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="071b5-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="071b5-122">Dit is vooral handig als u niet bekend bent met de navigatie in de portal nog.</span><span class="sxs-lookup"><span data-stu-id="071b5-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="071b5-123">Hallo volgende schermafbeelding is slechts een voorbeeld van hoe u uw MySQL-database kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="071b5-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Een MySQL-database maken in Azure - configureren](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="071b5-125">Wanneer u klaar bent configureren, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="071b5-125">When you're done configuring, click **Create**.</span></span>

    ![Een MySQL-database maken in Azure - maken](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="071b5-127">Hier ziet u een pop-upbericht waarin wordt aangegeven dat de implementatie is gestart.</span><span class="sxs-lookup"><span data-stu-id="071b5-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Maken van een MySQL-database in Azure - uitgevoerd](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="071b5-129">Krijgt u een andere pop-up zodra de implementatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="071b5-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="071b5-130">Hallo-portal wordt de blade van uw MySQL-database ook automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="071b5-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="071b5-131">Verbinding maken met tooyour MySQL-database</span><span class="sxs-lookup"><span data-stu-id="071b5-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="071b5-132">toosee Hallo-verbindingsgegevens voor de nieuwe MySQL-database, klikt u op **eigenschappen** in uw web-app-blade.</span><span class="sxs-lookup"><span data-stu-id="071b5-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Een MySQL-database maken in Azure - blade MySQL-database](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="071b5-134">U kunt nu verbindingsinformatie in een web-app.</span><span class="sxs-lookup"><span data-stu-id="071b5-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="071b5-135">Een steekproef die wordt weergegeven hoe toouse Hallo-verbindingsinformatie van een eenvoudige PHP-app beschikbaar is [hier](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="071b5-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="071b5-136">Verbinding maken met een Laravel web-app (uit Hallo PHP get gestart zelfstudie)</span><span class="sxs-lookup"><span data-stu-id="071b5-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="071b5-137">Stel dat u net klaar Hallo zelfstudie [maken, configureren en implementeren van een PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) en hebben een [Laravel](https://www.laravel.com/) web-app in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="071b5-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="071b5-138">U kunt eenvoudig database mogelijkheden tooyour Laravel app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="071b5-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="071b5-139">Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="071b5-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="071b5-140">Hallo volgende stappen wordt ervan uitgegaan dat u klaar bent met het Hallo-zelfstudie [maken, configureren en implementeren van een PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="071b5-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="071b5-141">Hallo Laravel app configureren in uw lokale ontwikkeling omgeving toopoint toohello MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="071b5-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="071b5-142">toodo deze, open `.env` de hoofdmap van uw Laravel-app en Hallo MySQL-database-opties configureren.</span><span class="sxs-lookup"><span data-stu-id="071b5-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="071b5-143">In Hallo **eigenschappen** blade Hallo-naam van uw MySQL-database mogelijk of worden mogelijk niet Hallo een weergegeven in Hallo **DATABASENAAM** veld.</span><span class="sxs-lookup"><span data-stu-id="071b5-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="071b5-144">Het is beter toocheck hello databaseparameter in Hallo **VERBINDINGSREEKS** veld.</span><span class="sxs-lookup"><span data-stu-id="071b5-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Maken van een MySQL-database in Azure - uitgevoerd](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="071b5-146">Hallo snelste manier tooverify dat u gemachtigd MySQL nu is toouse [Laravel van standaard verificatie steigers](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="071b5-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="071b5-147">Uitvoeren in Hallo opdrachtregelprogramma terminal Hallo volgende opdrachten uit de hoofdmap van uw app Laravel:</span><span class="sxs-lookup"><span data-stu-id="071b5-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="071b5-148">de eerste opdracht Hallo Hallo tabellen gemaakt in Azure op basis van vooraf gedefinieerde migraties in Hallo `database/migrations` directory en de tweede opdracht Hallo platforms Hallo basic weergaven en routes voor gebruikersregistratie en verificatie.</span><span class="sxs-lookup"><span data-stu-id="071b5-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="071b5-149">Hallo-ontwikkelaarsserver nu uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="071b5-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="071b5-150">Navigeer toohttp://localhost:8000 in Hallo browser en een nieuwe gebruiker registreren, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="071b5-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Verbinding maken met tooMySQL database in Azure - registreren van de gebruiker](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="071b5-152">Ga als volgt Hallo UI vragen voltooid Hallo registratie.</span><span class="sxs-lookup"><span data-stu-id="071b5-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="071b5-153">Wanneer de registratie is voltooid, wordt u vastgelegd in.</span><span class="sxs-lookup"><span data-stu-id="071b5-153">Once registration completes, you will be logged in.</span></span>

    ![Verbinding maken met tooMySQL database in Azure - registreren van de gebruiker](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="071b5-155">U nu ontwikkelt uw app op Hallo MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="071b5-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="071b5-156">Nu hoeft u alleen tooreplicate uw `.env` instellingen tooyour Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="071b5-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="071b5-157">Voer hello Azure CLI-opdrachten te volgen:</span><span class="sxs-lookup"><span data-stu-id="071b5-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="071b5-158">Vervolgens doorvoeren en push tooAzure Hallo lokale wijzigingen eerder tijdens de uitvoering `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="071b5-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="071b5-159">Blader toohello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="071b5-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="071b5-160">Meld u aan met de Hallo-gebruikersreferenties die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="071b5-160">Log in using hello user credentials you created earlier.</span></span>

    ![Verbinding maken met tooMySQL database in Azure - web-app tooAzure bladeren](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="071b5-162">Nadat u zich hebt aangemeld, ziet u beschrijvende na de aanmelding welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="071b5-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Verbinding maken met tooMySQL database in Azure - aangemeld](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="071b5-164">Gefeliciteerd, uw PHP-web-app in Azure is nu toegang tot gegevens uit uw MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="071b5-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="071b5-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="071b5-165">Next steps</span></span>
<span data-ttu-id="071b5-166">Zie voor meer informatie, Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="071b5-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
