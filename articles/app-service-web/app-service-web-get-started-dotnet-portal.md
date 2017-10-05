---
title: Binnen vijf minuten een Umbraco-web-app implementeren in Azure Portal | Microsoft Docs
description: Ontdek door implementatie van een ASP.NET-voorbeeld-app hoe eenvoudig het is om web-apps in App Service uit te voeren. U kunt direct de resultaten bekijken.
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
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="10de0-104">Binnen vijf minuten een Umbraco-web-app implementeren in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="10de0-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="10de0-105">Deze zelfstudie helpt u om binnen enkele minuten een [Umbraco](https://our.umbraco.org/)-web-app te implementeren in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="10de0-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco-app](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="10de0-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="10de0-107">Prerequisites</span></span>
<span data-ttu-id="10de0-108">U hebt een Microsoft Azure-account nodig.</span><span class="sxs-lookup"><span data-stu-id="10de0-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="10de0-109">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="10de0-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="10de0-110">U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="10de0-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="10de0-111">U kunt een beginnerstoepassing maken en hier een uur mee spelen. U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="10de0-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="10de0-112">De ASP.NET-app implementeren</span><span class="sxs-lookup"><span data-stu-id="10de0-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="10de0-113">Meld u aan bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10de0-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="10de0-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="10de0-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="10de0-115">Deze koppeling is een snelkoppeling waarmee u direct een nieuwe Umbraco-app kunt configureren in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="10de0-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="10de0-116">In **App-naam** voert u een naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="10de0-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="10de0-117">Er wordt een groen vinkje weergegeven in het vak als de naam uniek is in het domein `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="10de0-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="10de0-118">In **Resourcegroep** klikt u op **Nieuw** om een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) te maken. Geef de groep vervolgens een naam.</span><span class="sxs-lookup"><span data-stu-id="10de0-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="10de0-119">Klik op **App Service-plan/-locatie** > **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="10de0-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="10de0-120">Configureer het [App Service-plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) als volgt:</span><span class="sxs-lookup"><span data-stu-id="10de0-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="10de0-121">In **App Service-plan** voert u de gewenste naam in.</span><span class="sxs-lookup"><span data-stu-id="10de0-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="10de0-122">In **Locatie** kiest u een locatie voor het hosten van uw plan.</span><span class="sxs-lookup"><span data-stu-id="10de0-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="10de0-123">Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="10de0-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="10de0-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="10de0-124">Click **OK**.</span></span>

    <span data-ttu-id="10de0-125">De Umbraco CMS-configuratie ziet er nu uit als in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="10de0-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuratie in uitvoering - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="10de0-127">Klik op **SQL Database** > **Een nieuwe database maken**.</span><span class="sxs-lookup"><span data-stu-id="10de0-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="10de0-128">Configureer de SQL-database als volgt:</span><span class="sxs-lookup"><span data-stu-id="10de0-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="10de0-129">Voer in **Naam** een naam in, zoals **myDB**.</span><span class="sxs-lookup"><span data-stu-id="10de0-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="10de0-130">Klik op **Prijscategorie** en selecteer **F Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="10de0-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="10de0-131">Klik op **Doelserver** > **Een nieuwe server maken**.</span><span class="sxs-lookup"><span data-stu-id="10de0-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="10de0-132">Configureer de databaseserver als weergegeven:</span><span class="sxs-lookup"><span data-stu-id="10de0-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="10de0-133">Voer in **Servernaam** een servernaam in.</span><span class="sxs-lookup"><span data-stu-id="10de0-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="10de0-134">Er wordt een groen vinkje weergegeven in het vak als de naam uniek is in het domein `.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="10de0-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="10de0-135">In **Aanmeldgegevens van serverbeheerder** voert u de gewenste gebruikersnaam in voor de beheerder.</span><span class="sxs-lookup"><span data-stu-id="10de0-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="10de0-136">In **Wachtwoord** en **Wachtwoord bevestigen** voert u het gewenste wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="10de0-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="10de0-137">In Locatie selecteert u de locatie die u wilt gebruiken voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="10de0-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="10de0-138">Zorg ervoor dat **Toegang van Azure-services tot server toestaan** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="10de0-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="10de0-139">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="10de0-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="10de0-140">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="10de0-140">Click **Select**.</span></span>

13. <span data-ttu-id="10de0-141">Klik op **Web-app-instellingen**, geef een gebruikersnaam en wachtwoord op voor de database en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="10de0-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="10de0-142">De Umbraco CMS-configuratie ziet er nu uit als in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="10de0-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuratie voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="10de0-144">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="10de0-144">Click **Create**.</span></span>
    
    <span data-ttu-id="10de0-145">Azure maakt nu uw Umbraco-app op basis van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="10de0-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="10de0-146">De melding **Implementatie is gestart...** wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="10de0-146">You should see a **Deployment started...** notification.</span></span>

    ![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="10de0-148">Uw Umbraco-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="10de0-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="10de0-149">Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.</span><span class="sxs-lookup"><span data-stu-id="10de0-149">When Azure completes app deployment you see another notification.</span></span>

![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="10de0-151">Klik op de melding.</span><span class="sxs-lookup"><span data-stu-id="10de0-151">Click the notification.</span></span> <span data-ttu-id="10de0-152">Als u de melding hebt gemist, kunt u deze altijd openen door op de bel te klikken (![Melding onderaan - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="10de0-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="10de0-153">U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).</span><span class="sxs-lookup"><span data-stu-id="10de0-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="10de0-154">Klik boven aan de pagina Overzicht op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="10de0-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Bladeren - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="10de0-156">U ziet de **welkomstpagina** van Umbraco.</span><span class="sxs-lookup"><span data-stu-id="10de0-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="10de0-157">Configureer de Umbraco-installatie en ga ermee aan de slag!</span><span class="sxs-lookup"><span data-stu-id="10de0-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Umbraco-configuratie - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="10de0-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10de0-159">Next steps</span></span>
* <span data-ttu-id="10de0-160">[Een ASP.NET-web-app in Azure App Service implementeren met Visual Studio](app-service-web-get-started-dotnet.md) -Informatie over het maken van een nieuwe Azure-web-app via Visual Studio met behulp van één van de meegeleverde toepassingssjablonen.</span><span class="sxs-lookup"><span data-stu-id="10de0-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="10de0-161">[Uw code implementeren in Azure App Service](web-sites-deploy.md) - Informatie over implementeren via FTP of via broncodebeheeropslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="10de0-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="10de0-162">[Functionaliteit toevoegen aan uw eerste web-app](app-service-web-get-started-2.md) - Til uw Azure-app naar een hoger niveau.</span><span class="sxs-lookup"><span data-stu-id="10de0-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="10de0-163">Verifieer uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="10de0-163">Authenticate your users.</span></span> <span data-ttu-id="10de0-164">Schaal de app op basis van vraag.</span><span class="sxs-lookup"><span data-stu-id="10de0-164">Scale it based on demand.</span></span> <span data-ttu-id="10de0-165">Stel prestatiewaarschuwingen in.</span><span class="sxs-lookup"><span data-stu-id="10de0-165">Set up some performance alerts.</span></span> <span data-ttu-id="10de0-166">Dit alles met slechts enkele klikken.</span><span class="sxs-lookup"><span data-stu-id="10de0-166">All with a few clicks.</span></span>
