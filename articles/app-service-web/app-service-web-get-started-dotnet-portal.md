---
title: een Umbraco web-app in Azure-portal op vijf minuten Hallo aaaDeploy | Microsoft Docs
description: Informatie over hoe eenvoudig het is toorun web-apps in App Service door het implementeren van een voorbeeld van ASP.NET-app. U kunt direct de resultaten bekijken.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="7da28-104">Een Umbraco web-app in Azure-portal Hallo implementeren binnen vijf minuten</span><span class="sxs-lookup"><span data-stu-id="7da28-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="7da28-105">Deze zelfstudie helpt u n implementeren [Umbraco](https://our.umbraco.org/) web-app te[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuten.</span><span class="sxs-lookup"><span data-stu-id="7da28-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco-app](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="7da28-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7da28-107">Prerequisites</span></span>
<span data-ttu-id="7da28-108">U hebt een Microsoft Azure-account nodig.</span><span class="sxs-lookup"><span data-stu-id="7da28-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="7da28-109">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="7da28-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="7da28-110">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7da28-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="7da28-111">Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="7da28-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="7da28-112">Hallo ASP.NET-app implementeren</span><span class="sxs-lookup"><span data-stu-id="7da28-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="7da28-113">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7da28-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7da28-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="7da28-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="7da28-115">Deze koppeling is een snelkoppeling tooimmediately configureren een nieuwe Umbraco-app in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7da28-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="7da28-116">In **App-naam** voert u een naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="7da28-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="7da28-117">U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `azurewebsites.net` domein.</span><span class="sxs-lookup"><span data-stu-id="7da28-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="7da28-118">In **resourcegroep**, klikt u op **nieuw** toocreate een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md), geef het een naam.</span><span class="sxs-lookup"><span data-stu-id="7da28-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="7da28-119">Klik op **App Service-plan/-locatie** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="7da28-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="7da28-120">Hallo configureren [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7da28-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="7da28-121">In **App Service-abonnement**, Hallo gewenste typenaam.</span><span class="sxs-lookup"><span data-stu-id="7da28-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="7da28-122">In **locatie**, kies een locatie toohost uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7da28-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="7da28-123">Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7da28-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="7da28-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da28-124">Click **OK**.</span></span>

    <span data-ttu-id="7da28-125">De configuratie van uw Umbraco CMS ziet er nu als Hallo schermafbeelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da28-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuratie in uitvoering - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="7da28-127">Klik op **SQL Database** > **Een nieuwe database maken**.</span><span class="sxs-lookup"><span data-stu-id="7da28-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="7da28-128">Hallo SQL-Database configureren zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7da28-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="7da28-129">Voer in **Naam** een naam in, zoals **myDB**.</span><span class="sxs-lookup"><span data-stu-id="7da28-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="7da28-130">Klik op **Prijscategorie** en selecteer **F Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7da28-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="7da28-131">Klik op **Doelserver** > **Een nieuwe server maken**.</span><span class="sxs-lookup"><span data-stu-id="7da28-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="7da28-132">Hallo-databaseserver configureren zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7da28-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="7da28-133">Voer in **Servernaam** een servernaam in.</span><span class="sxs-lookup"><span data-stu-id="7da28-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="7da28-134">U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `.database.windows.net` domein.</span><span class="sxs-lookup"><span data-stu-id="7da28-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="7da28-135">In **aanmeldgegevens van serverbeheerder**, type Hallo beheerder gebruikersnaam gewenst.</span><span class="sxs-lookup"><span data-stu-id="7da28-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="7da28-136">In **wachtwoord** en **wachtwoord bevestigen**, type Hallo gewenste wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7da28-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="7da28-137">Selecteer Hallo op locatie, dezelfde locatie die u voor Hallo web-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7da28-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="7da28-138">Zorg ervoor dat **toestaan azure-services tooaccess server** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7da28-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="7da28-139">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7da28-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="7da28-140">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7da28-140">Click **Select**.</span></span>

13. <span data-ttu-id="7da28-141">Klik op **Web-appinstellingen**Hallo database een gebruikersnaam en wachtwoord opgeven en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7da28-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="7da28-142">De configuratie van uw Umbraco CMS ziet er nu als Hallo schermafbeelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="7da28-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuratie voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="7da28-144">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7da28-144">Click **Create**.</span></span>
    
    <span data-ttu-id="7da28-145">Azure maakt nu uw Umbraco-app op basis van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="7da28-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="7da28-146">De melding **Implementatie is gestart...** wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7da28-146">You should see a **Deployment started...** notification.</span></span>

    ![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="7da28-148">Uw Umbraco-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="7da28-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="7da28-149">Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.</span><span class="sxs-lookup"><span data-stu-id="7da28-149">When Azure completes app deployment you see another notification.</span></span>

![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="7da28-151">Klik op Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="7da28-151">Click hello notification.</span></span> <span data-ttu-id="7da28-152">Als u deze hebt gemist, u kunt altijd toegang tot dit door te klikken op Hallo melding Bel (![melding onderstaande - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="7da28-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="7da28-153">U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).</span><span class="sxs-lookup"><span data-stu-id="7da28-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="7da28-154">Klik in het Hallo bovenaan de pagina overzicht Hallo op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="7da28-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Bladeren - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="7da28-156">Nu u Hallo Umbraco ziet **Welkom** pagina.</span><span class="sxs-lookup"><span data-stu-id="7da28-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="7da28-157">Hallo Umbraco installatie configureren en begin met het afspelen.</span><span class="sxs-lookup"><span data-stu-id="7da28-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Umbraco-configuratie - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="7da28-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7da28-159">Next steps</span></span>
* <span data-ttu-id="7da28-160">[Een ASP.NET web app tooAzure App Service met Visual Studio implementeren](app-service-web-get-started-dotnet.md) -informatie over hoe een nieuwe Azure-web-app vanuit Visual Studio, met een van de Hallo toocreate Toepassingssjablonen opgenomen.</span><span class="sxs-lookup"><span data-stu-id="7da28-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="7da28-161">[Uw code tooAzure App Service implementeren](web-sites-deploy.md)-informatie over hoe de opslagplaatsen voor het beheren van toodeploy van FTP- of bron.</span><span class="sxs-lookup"><span data-stu-id="7da28-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="7da28-162">[Functionaliteit tooyour eerste web-app toevoegen](app-service-web-get-started-2.md) -Til uw Azure-app toohello naast niveau.</span><span class="sxs-lookup"><span data-stu-id="7da28-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="7da28-163">Verifieer uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7da28-163">Authenticate your users.</span></span> <span data-ttu-id="7da28-164">Schaal de app op basis van vraag.</span><span class="sxs-lookup"><span data-stu-id="7da28-164">Scale it based on demand.</span></span> <span data-ttu-id="7da28-165">Stel prestatiewaarschuwingen in.</span><span class="sxs-lookup"><span data-stu-id="7da28-165">Set up some performance alerts.</span></span> <span data-ttu-id="7da28-166">Dit alles met slechts enkele klikken.</span><span class="sxs-lookup"><span data-stu-id="7da28-166">All with a few clicks.</span></span>
