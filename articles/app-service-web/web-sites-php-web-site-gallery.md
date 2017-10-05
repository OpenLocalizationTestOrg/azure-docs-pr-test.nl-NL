---
title: Een WordPress-web-app maken in Azure App Service | Microsoft Docs
description: Ontdek hoe u via Azure Portal een nieuwe Azure-web-app maakt voor een WordPress-blog.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="cf931-103">Een WordPress-web-app maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cf931-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="cf931-104">In deze zelfstudie gaat u een WordPress-blogsite implementeren vanuit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf931-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="cf931-105">Wanneer u de zelfstudie hebt voltooid, hebt u uw eigen WordPress-site in de cloud.</span><span class="sxs-lookup"><span data-stu-id="cf931-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="cf931-107">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="cf931-107">You'll learn:</span></span>

* <span data-ttu-id="cf931-108">Een toepassingssjabloon zoeken in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf931-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="cf931-109">In Azure App Service een web-app maken die op de sjabloon is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="cf931-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="cf931-110">Azure App Service-instellingen configureren voor de nieuwe web-app en database.</span><span class="sxs-lookup"><span data-stu-id="cf931-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="cf931-111">Azure Marketplace maakt een groot aantal populaire web-apps beschikbaar die zijn ontwikkeld door Microsoft, door derden of via OOS-initiatieven (Open Source Software).</span><span class="sxs-lookup"><span data-stu-id="cf931-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="cf931-112">De web-apps zijn gebouwd op een breed scala aan populaire frameworks, zoals [PHP](/develop/nodejs/) in dit WordPress-voorbeeld, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) en [Python](/develop/python/), om er enkele te noemen.</span><span class="sxs-lookup"><span data-stu-id="cf931-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="cf931-113">De enige software die u nodig hebt om vanuit Azure Marketplace een web-app te maken, is de browser die u gebruikt voor de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf931-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="cf931-114">Op de WordPress-site die u in deze zelfstudie gaat implementeren, wordt voor de database MySQL gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cf931-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="cf931-115">Als u in plaats daarvan voor de database SQL Database wilt gebruiken, raadpleegt u [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="cf931-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="cf931-116">**Project Nami** is ook beschikbaar via de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf931-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="cf931-117">U hebt een Microsoft Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="cf931-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="cf931-118">Als u geen account hebt, kunt u [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) of [zich aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="cf931-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="cf931-119">Als u met Azure App Service aan de slag wilt voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="cf931-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="cf931-120">Daar kunt u direct een eenvoudige, tijdelijke web-app maken in App Service. U hebt hiervoor geen creditcard nodig en bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="cf931-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="cf931-121">WordPress selecteren en configureren voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cf931-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="cf931-122">Meld u aan bij de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf931-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf931-123">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="cf931-123">Click **New**.</span></span>
   
    ![Nieuwe maken][5]
3. <span data-ttu-id="cf931-125">Zoek naar **WordPress** en klik op **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="cf931-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="cf931-126">Als u in plaats van MySQL SQL Database wilt gebruiken, zoekt u naar **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="cf931-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress via een lijst][7]
4. <span data-ttu-id="cf931-128">Lees de beschrijving van de WordPress-app en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="cf931-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Maken](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="cf931-130">Typ in het vak **Web-app** een naam voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="cf931-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="cf931-131">Deze naam moet uniek zijn in het domein azurewebsites.net, omdat de URL van de web-app {naam}.azurewebsites.net wordt.</span><span class="sxs-lookup"><span data-stu-id="cf931-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="cf931-132">Als de ingevoerde naam niet uniek is, ziet u een rood uitroepteken in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="cf931-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="cf931-133">Als u meerdere abonnementen hebt, kiest u het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cf931-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="cf931-134">Selecteer een **Resourcegroep** of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="cf931-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="cf931-135">Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="cf931-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="cf931-136">Selecteer een **App Service-plan/-locatie** of maak een nieuw(e).</span><span class="sxs-lookup"><span data-stu-id="cf931-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="cf931-137">Zie [Overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor meer informatie over App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="cf931-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="cf931-138">Klik op **Database** en geef op de blade **Nieuwe MySQL-database** de vereiste waarden op om uw MySQL-database te configureren.</span><span class="sxs-lookup"><span data-stu-id="cf931-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="cf931-139">a.</span><span class="sxs-lookup"><span data-stu-id="cf931-139">a.</span></span> <span data-ttu-id="cf931-140">Voer een nieuwe naam in of laat de standaardnaam staan.</span><span class="sxs-lookup"><span data-stu-id="cf931-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="cf931-141">b.</span><span class="sxs-lookup"><span data-stu-id="cf931-141">b.</span></span> <span data-ttu-id="cf931-142">Laat **Databasetype** ingesteld op **Gedeeld**.</span><span class="sxs-lookup"><span data-stu-id="cf931-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="cf931-143">c.</span><span class="sxs-lookup"><span data-stu-id="cf931-143">c.</span></span> <span data-ttu-id="cf931-144">Kies de locatie die u ook voor de web-app hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="cf931-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="cf931-145">d.</span><span class="sxs-lookup"><span data-stu-id="cf931-145">d.</span></span> <span data-ttu-id="cf931-146">Kies een prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="cf931-146">Choose a pricing tier.</span></span> <span data-ttu-id="cf931-147">Mercury (gratis met minimale verbindingen en schijfruimte) is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cf931-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="cf931-148">Klik op de blade **Nieuwe MySQL-database** op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf931-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="cf931-149">Accepteer de juridische bepalingen op de blade **WordPress** en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="cf931-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Web-app configureren](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="cf931-151">De web-app wordt gewoonlijk in nog geen minuut door Azure App Service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf931-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="cf931-152">U kunt de voortgang bekijken door boven aan de portalpagina op het belpictogram te klikken.</span><span class="sxs-lookup"><span data-stu-id="cf931-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Voortgangsindicator](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="cf931-154">De WordPress-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="cf931-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="cf931-155">Wanneer de web-app is gemaakt, navigeert u in Azure Portal naar de resourcegroep waarin u de toepassing hebt gemaakt. Hier ziet u de web-app en de database.</span><span class="sxs-lookup"><span data-stu-id="cf931-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="cf931-156">De extra resource met het pictogram van een gloeilampje is [Application Insights](/services/application-insights/), een resource die bewakingsservices voor uw web-app biedt.</span><span class="sxs-lookup"><span data-stu-id="cf931-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="cf931-157">Klik op de blade **Resourcegroep** op de regel van de web-app.</span><span class="sxs-lookup"><span data-stu-id="cf931-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Web-app configureren](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="cf931-159">Klik op de blade Web-apps op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="cf931-159">In the Web app blade, click **Browse**.</span></span>
   
    ![site-URL][browse]
4. <span data-ttu-id="cf931-161">Voer op de **Welkomstpagina** van WordPress de configuratiegegevens in die WordPress nodig heeft. Klik vervolgens op **WordPress installeren**.</span><span class="sxs-lookup"><span data-stu-id="cf931-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress configureren](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="cf931-163">Meld u aan met de referenties die u op de **Welkomstpagina** hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf931-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="cf931-164">De dashboardpagina van uw site wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="cf931-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="cf931-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf931-166">Next steps</span></span>
<span data-ttu-id="cf931-167">U hebt gezien hoe u een PHP-web-app uit de galerie maakt en implementeert.</span><span class="sxs-lookup"><span data-stu-id="cf931-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="cf931-168">In het [PHP-ontwikkelaarscentrum](/develop/php/) vindt u meer informatie over het gebruik van PHP in Azure.</span><span class="sxs-lookup"><span data-stu-id="cf931-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="cf931-169">Voor meer informatie over werken met App Service-web-apps klikt u op de koppelingen aan de linkerkant van de pagina (in brede browservensters) of boven aan de pagina (in smalle browservensters).</span><span class="sxs-lookup"><span data-stu-id="cf931-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="cf931-170">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="cf931-170">What's changed</span></span>
* <span data-ttu-id="cf931-171">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cf931-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
