---
title: Binnen vijf minuten een WordPress-app implementeren in Azure Portal | Microsoft Docs
description: Hier ontdekt u door een WordPress-app te implementeren hoe eenvoudig het is om web-apps in App Service uit te voeren. U kunt direct de resultaten bekijken.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="adfc7-104">Binnen vijf minuten een WordPress-app implementeren in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="adfc7-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="adfc7-105">In deze zelfstudie ziet u hoe u binnen slechts enkele minuten uw eerste [WordPress](https://wordpress.org/)-web-app implementeert in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="adfc7-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress-site](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="adfc7-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="adfc7-107">Prerequisites</span></span>
<span data-ttu-id="adfc7-108">U hebt een Microsoft Azure-account nodig.</span><span class="sxs-lookup"><span data-stu-id="adfc7-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="adfc7-109">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="adfc7-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="adfc7-110">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="adfc7-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="adfc7-111">U kunt een beginnerstoepassing maken en hier een uur mee spelen. U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="adfc7-112">De WordPress-app implementeren</span><span class="sxs-lookup"><span data-stu-id="adfc7-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="adfc7-113">Meld u aan bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adfc7-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="adfc7-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="adfc7-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="adfc7-115">Deze koppeling is een snelkoppeling waarmee u direct een nieuwe WordPress-app kunt configureren in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="adfc7-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="adfc7-116">In **App-naam** voert u een naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="adfc7-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="adfc7-117">Er wordt een groen vinkje weergegeven in het vak als de naam uniek is in het domein `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="adfc7-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="adfc7-118">In **Resourcegroep** klikt u op **Nieuw** om een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) te maken. Geef de groep vervolgens een naam.</span><span class="sxs-lookup"><span data-stu-id="adfc7-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="adfc7-119">In **Databaseprovider** selecteert u **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="adfc7-120">Klik op **App Service-plan/-locatie** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="adfc7-121">Configureer het [App Service-plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) als volgt:</span><span class="sxs-lookup"><span data-stu-id="adfc7-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="adfc7-122">In **App Service-plan** voert u de gewenste naam in.</span><span class="sxs-lookup"><span data-stu-id="adfc7-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="adfc7-123">In **Locatie** kiest u een locatie voor het hosten van uw plan.</span><span class="sxs-lookup"><span data-stu-id="adfc7-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="adfc7-124">Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="adfc7-125">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-125">Click **OK**.</span></span>

8. <span data-ttu-id="adfc7-126">Klik op **Database** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="adfc7-127">Configureer de SQL-database als volgt:</span><span class="sxs-lookup"><span data-stu-id="adfc7-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="adfc7-128">In **Databasenaam** voert u een naam in voor de database.</span><span class="sxs-lookup"><span data-stu-id="adfc7-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="adfc7-129">In **Locatie** kiest u dezelfde locatie als voor het App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="adfc7-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="adfc7-130">Klik op **Prijscategorie** en selecteer **Mercury** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="adfc7-131">Klik op **Juridische voorwaarden** en klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="adfc7-132">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-132">Click **OK**.</span></span>

9. <span data-ttu-id="adfc7-133">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-133">Click **Create**.</span></span>

    <span data-ttu-id="adfc7-134">Azure maakt nu uw WordPress-app op basis van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="adfc7-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="adfc7-135">De melding **Implementatie is gestart...** wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="adfc7-135">You should see a **Deployment started...** notification.</span></span>

    ![De implementatie is gestart - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="adfc7-137">De WordPress-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="adfc7-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="adfc7-138">Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.</span><span class="sxs-lookup"><span data-stu-id="adfc7-138">When Azure completes app deployment you see another notification.</span></span>

![De implementatie is voltooid - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="adfc7-140">Klik op de melding.</span><span class="sxs-lookup"><span data-stu-id="adfc7-140">Click the notification.</span></span> <span data-ttu-id="adfc7-141">Als u de melding hebt gemist, kunt u deze altijd openen door op de bel te klikken (![Melding onderaan - eerste WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="adfc7-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="adfc7-142">U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).</span><span class="sxs-lookup"><span data-stu-id="adfc7-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="adfc7-143">Klik boven aan de pagina Overzicht op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="adfc7-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Bladeren - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="adfc7-145">U ziet de **welkomstpagina** van WordPress.</span><span class="sxs-lookup"><span data-stu-id="adfc7-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="adfc7-146">Configureer de WordPress-installatie en ga ermee aan de slag!</span><span class="sxs-lookup"><span data-stu-id="adfc7-146">Configure the WordPress installation and start playing with it!</span></span>

    ![Configuratie van WordPress - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="adfc7-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adfc7-148">Next steps</span></span>
* <span data-ttu-id="adfc7-149">[Een Laravel-web-app maken, configureren en implementeren in Azure](app-service-web-php-get-started.md) - Informatie over de algemene vaardigheden die nodig zijn voor het uitvoeren van PHP-web-apps in Azure, zoals:</span><span class="sxs-lookup"><span data-stu-id="adfc7-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="adfc7-150">Apps via PowerShell/Bash maken en configureren in Azure.</span><span class="sxs-lookup"><span data-stu-id="adfc7-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="adfc7-151">De PHP-versie instellen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-151">Set PHP version.</span></span>
    * <span data-ttu-id="adfc7-152">Een opstartbestand gebruiken dat zich niet in de hoofdmap van de toepassing bevindt.</span><span class="sxs-lookup"><span data-stu-id="adfc7-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="adfc7-153">Composer-automatisering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="adfc7-154">Omgevingsspecifieke variabelen openen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="adfc7-155">Veelvoorkomende problemen oplossen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="adfc7-156">[Uw code implementeren in Azure App Service](web-sites-deploy.md) - Informatie over implementeren via FTP of via broncodebeheeropslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="adfc7-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="adfc7-157">[Functionaliteit toevoegen aan uw eerste web-app](app-service-web-get-started-2.md) - Til uw Azure-app naar een hoger niveau.</span><span class="sxs-lookup"><span data-stu-id="adfc7-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="adfc7-158">Verifieer uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="adfc7-158">Authenticate your users.</span></span> <span data-ttu-id="adfc7-159">Schaal de app op basis van vraag.</span><span class="sxs-lookup"><span data-stu-id="adfc7-159">Scale it based on demand.</span></span> <span data-ttu-id="adfc7-160">Stel prestatiewaarschuwingen in.</span><span class="sxs-lookup"><span data-stu-id="adfc7-160">Set up some performance alerts.</span></span> <span data-ttu-id="adfc7-161">Dit alles met slechts enkele klikken.</span><span class="sxs-lookup"><span data-stu-id="adfc7-161">All with a few clicks.</span></span>
