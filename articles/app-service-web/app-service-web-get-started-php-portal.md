---
title: een WordPress-app in Azure-portal op vijf minuten Hallo aaaDeploy | Microsoft Docs
description: Informatie over hoe eenvoudig het is toorun web-apps in App Service door het implementeren van een WordPress-app. U kunt direct de resultaten bekijken.
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
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="4760e-104">Een WordPress-app in Azure-portal Hallo implementeren binnen vijf minuten</span><span class="sxs-lookup"><span data-stu-id="4760e-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="4760e-105">Deze zelfstudie leert u hoe toodeploy uw eerste [WordPress](https://wordpress.org/) web-app te[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuten.</span><span class="sxs-lookup"><span data-stu-id="4760e-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress-site](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="4760e-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4760e-107">Prerequisites</span></span>
<span data-ttu-id="4760e-108">U hebt een Microsoft Azure-account nodig.</span><span class="sxs-lookup"><span data-stu-id="4760e-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="4760e-109">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4760e-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="4760e-110">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4760e-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="4760e-111">Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="4760e-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="4760e-112">Hallo WordPress-app implementeren</span><span class="sxs-lookup"><span data-stu-id="4760e-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="4760e-113">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4760e-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4760e-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="4760e-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="4760e-115">Deze koppeling is een snelkoppeling tooimmediately configureren een nieuwe WordPress-app in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4760e-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="4760e-116">In **App-naam** voert u een naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="4760e-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="4760e-117">U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `azurewebsites.net` domein.</span><span class="sxs-lookup"><span data-stu-id="4760e-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="4760e-118">In **resourcegroep**, klikt u op **nieuw** toocreate een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md), geef het een naam.</span><span class="sxs-lookup"><span data-stu-id="4760e-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="4760e-119">In **Databaseprovider** selecteert u **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="4760e-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="4760e-120">Klik op **App Service-plan/-locatie** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="4760e-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="4760e-121">Hallo configureren [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4760e-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="4760e-122">In **App Service-abonnement**, Hallo gewenste typenaam.</span><span class="sxs-lookup"><span data-stu-id="4760e-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="4760e-123">In **locatie**, kies een locatie toohost uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4760e-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="4760e-124">Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="4760e-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="4760e-125">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4760e-125">Click **OK**.</span></span>

8. <span data-ttu-id="4760e-126">Klik op **Database** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="4760e-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="4760e-127">Hallo SQL-Database configureren zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4760e-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="4760e-128">In **Databasenaam** voert u een naam in voor de database.</span><span class="sxs-lookup"><span data-stu-id="4760e-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="4760e-129">In **locatie**, kies Hallo dezelfde locatie als Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4760e-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="4760e-130">Klik op **Prijscategorie** en selecteer **Mercury** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="4760e-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="4760e-131">Klik op **Juridische voorwaarden** en klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="4760e-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="4760e-132">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4760e-132">Click **OK**.</span></span>

9. <span data-ttu-id="4760e-133">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4760e-133">Click **Create**.</span></span>

    <span data-ttu-id="4760e-134">Azure maakt nu uw WordPress-app op basis van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="4760e-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="4760e-135">De melding **Implementatie is gestart...** wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4760e-135">You should see a **Deployment started...** notification.</span></span>

    ![De implementatie is gestart - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="4760e-137">De WordPress-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="4760e-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="4760e-138">Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.</span><span class="sxs-lookup"><span data-stu-id="4760e-138">When Azure completes app deployment you see another notification.</span></span>

![De implementatie is voltooid - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="4760e-140">Klik op Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="4760e-140">Click hello notification.</span></span> <span data-ttu-id="4760e-141">Als u deze hebt gemist, u kunt altijd toegang tot dit door te klikken op Hallo melding Bel (![melding onderstaande - eerste WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="4760e-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="4760e-142">U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).</span><span class="sxs-lookup"><span data-stu-id="4760e-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="4760e-143">Klik in het Hallo bovenaan de pagina overzicht Hallo op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="4760e-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Bladeren - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="4760e-145">Nu u Hallo WordPress ziet **Welkom** pagina.</span><span class="sxs-lookup"><span data-stu-id="4760e-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="4760e-146">Hallo WordPress installatie configureren en begin met het afspelen.</span><span class="sxs-lookup"><span data-stu-id="4760e-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Configuratie van WordPress - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="4760e-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4760e-148">Next steps</span></span>
* <span data-ttu-id="4760e-149">[Maken, configureren en implementeren van een Laravel web app tooAzure](app-service-web-php-get-started.md) -meer Hallo basisvaardigheden moet u toorun een PHP-web-app in Azure, zoals:</span><span class="sxs-lookup"><span data-stu-id="4760e-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="4760e-150">Apps via PowerShell/Bash maken en configureren in Azure.</span><span class="sxs-lookup"><span data-stu-id="4760e-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="4760e-151">De PHP-versie instellen.</span><span class="sxs-lookup"><span data-stu-id="4760e-151">Set PHP version.</span></span>
    * <span data-ttu-id="4760e-152">Een begin-bestand dat zich niet in de hoofdmap toepassing hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4760e-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="4760e-153">Composer-automatisering inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4760e-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="4760e-154">Omgevingsspecifieke variabelen openen.</span><span class="sxs-lookup"><span data-stu-id="4760e-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="4760e-155">Veelvoorkomende problemen oplossen.</span><span class="sxs-lookup"><span data-stu-id="4760e-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="4760e-156">[Uw code tooAzure App Service implementeren](web-sites-deploy.md)-informatie over hoe de opslagplaatsen voor het beheren van toodeploy van FTP- of bron.</span><span class="sxs-lookup"><span data-stu-id="4760e-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="4760e-157">[Functionaliteit tooyour eerste web-app toevoegen](app-service-web-get-started-2.md) -Til uw Azure-app toohello naast niveau.</span><span class="sxs-lookup"><span data-stu-id="4760e-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="4760e-158">Verifieer uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4760e-158">Authenticate your users.</span></span> <span data-ttu-id="4760e-159">Schaal de app op basis van vraag.</span><span class="sxs-lookup"><span data-stu-id="4760e-159">Scale it based on demand.</span></span> <span data-ttu-id="4760e-160">Stel prestatiewaarschuwingen in.</span><span class="sxs-lookup"><span data-stu-id="4760e-160">Set up some performance alerts.</span></span> <span data-ttu-id="4760e-161">Dit alles met slechts enkele klikken.</span><span class="sxs-lookup"><span data-stu-id="4760e-161">All with a few clicks.</span></span>
