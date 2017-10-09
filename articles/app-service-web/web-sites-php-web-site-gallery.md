---
title: aaaCreate een WordPress-web-app in Azure App Service | Microsoft Docs
description: Meer informatie over hoe een nieuwe Azure toocreate web-app voor een WordPress-blog hello Azure Portal gebruiken.
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
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="f4e90-103">Een WordPress-web-app maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4e90-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="f4e90-104">Deze zelfstudie laat zien hoe een WordPress-blog toodeploy site van hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4e90-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="f4e90-105">Wanneer u met het Hallo-zelfstudie bent klaar hebt u uw eigen WordPress-blogsite up en wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4e90-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="f4e90-107">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="f4e90-107">You'll learn:</span></span>

* <span data-ttu-id="f4e90-108">Hoe toofind een toepassingssjabloon in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4e90-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="f4e90-109">Hoe toocreate een web-app in Azure App Service die is gebaseerd op Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f4e90-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="f4e90-110">Hoe tooconfigure Azure App Service-instellingen voor Hallo nieuwe web-app en database.</span><span class="sxs-lookup"><span data-stu-id="f4e90-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="f4e90-111">Hello Azure Marketplace maakt beschikbaar een breed scala aan populaire web-apps die zijn ontwikkeld door Microsoft en derden bedrijven open-source software initiatieven.</span><span class="sxs-lookup"><span data-stu-id="f4e90-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="f4e90-112">Hallo-web-apps zijn gebouwd op een breed scala aan populaire frameworks, zoals [PHP](/develop/nodejs/) in dit WordPress-voorbeeld [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), en [Python](/develop/python/), tooname een enkele.</span><span class="sxs-lookup"><span data-stu-id="f4e90-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="f4e90-113">een web-app vanuit Azure Marketplace Hallo enige software die u nodig is Hallo browser die u voor Hallo gebruikt Hallo toocreate [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f4e90-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="f4e90-114">Hallo WordPress-site die u in deze zelfstudie implementeert maakt gebruik van MySQL voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f4e90-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="f4e90-115">Als u tooinstead SQL-Database gebruiken voor Hallo-database wenst, Zie [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="f4e90-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="f4e90-116">**Project Nami** is ook beschikbaar via Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4e90-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="f4e90-117">toocomplete deze zelfstudie maakt u een Microsoft Azure-account nodig.</span><span class="sxs-lookup"><span data-stu-id="f4e90-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="f4e90-118">Als u geen account hebt, kunt u [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) of [zich aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f4e90-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="f4e90-119">Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f4e90-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="f4e90-120">Daar kunt u direct een eenvoudige, tijdelijke web-app maken in App Service. U hebt hiervoor geen creditcard nodig en bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="f4e90-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="f4e90-121">WordPress selecteren en configureren voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4e90-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="f4e90-122">Meld u bij toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f4e90-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f4e90-123">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-123">Click **New**.</span></span>
   
    ![Nieuwe maken][5]
3. <span data-ttu-id="f4e90-125">Zoek naar **WordPress** en klik op **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="f4e90-126">Als u toouse SQL-Database in plaats van MySQL wenst, zoekt u naar **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress via een lijst][7]
4. <span data-ttu-id="f4e90-128">Klik na het lezen van Hallo beschrijving van Hallo WordPress-app op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Maken](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="f4e90-130">Voer een naam voor de web-app Hallo in Hallo **Web-app** vak.</span><span class="sxs-lookup"><span data-stu-id="f4e90-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="f4e90-131">Deze naam moet uniek zijn in Hallo azurewebsites.net domein omdat Hallo-URL van Hallo web-app {naam}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f4e90-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="f4e90-132">Als Hallo-naam die u opgeeft niet uniek is, wordt een rood uitroepteken in het tekstvak Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4e90-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="f4e90-133">Als u meer dan één abonnement hebt, kiest u Hallo één gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="f4e90-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="f4e90-134">Selecteer een **Resourcegroep** of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="f4e90-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="f4e90-135">Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="f4e90-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="f4e90-136">Selecteer een **App Service-plan/-locatie** of maak een nieuw(e).</span><span class="sxs-lookup"><span data-stu-id="f4e90-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="f4e90-137">Zie [Overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor meer informatie over App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="f4e90-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="f4e90-138">Klik op **Database**, en klik vervolgens in Hallo **nieuwe MySQL-Database** blade Hallo vereist waarden opgeven voor het configureren van uw MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="f4e90-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="f4e90-139">a.</span><span class="sxs-lookup"><span data-stu-id="f4e90-139">a.</span></span> <span data-ttu-id="f4e90-140">Voer een nieuwe naam op of laat de standaardnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4e90-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="f4e90-141">b.</span><span class="sxs-lookup"><span data-stu-id="f4e90-141">b.</span></span> <span data-ttu-id="f4e90-142">Hallo laat **databasetype** instellen te**gedeelde**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="f4e90-143">c.</span><span class="sxs-lookup"><span data-stu-id="f4e90-143">c.</span></span> <span data-ttu-id="f4e90-144">Kies Hallo dezelfde locatie als u één Hallo voor Hallo web-app hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="f4e90-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="f4e90-145">d.</span><span class="sxs-lookup"><span data-stu-id="f4e90-145">d.</span></span> <span data-ttu-id="f4e90-146">Kies een prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f4e90-146">Choose a pricing tier.</span></span> <span data-ttu-id="f4e90-147">Mercury (gratis met minimale verbindingen en schijfruimte) is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f4e90-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="f4e90-148">In Hallo **nieuwe MySQL-Database** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="f4e90-149">In Hallo **WordPress** blade Hallo juridische voorwaarden accepteren en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Web-app configureren](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="f4e90-151">Azure App Service gemaakt Hallo web-app, doorgaans in minder dan een minuut.</span><span class="sxs-lookup"><span data-stu-id="f4e90-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="f4e90-152">U kunt Hallo voortgang bekijken door te klikken op het belpictogram Hallo HALLO hallo portal-pagina bovenaan in.</span><span class="sxs-lookup"><span data-stu-id="f4e90-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Voortgangsindicator](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="f4e90-154">De WordPress-web-app starten en beheren</span><span class="sxs-lookup"><span data-stu-id="f4e90-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="f4e90-155">Wanneer Hallo web-apps maken is voltooid, gaat u in hello Azure Portal toohello resourcegroep waarin u Hallo toepassing gemaakt en ziet u Hallo web-app en het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f4e90-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="f4e90-156">Hallo extra resource met Hallo gloeilampje is [Application Insights](/services/application-insights/), die bewakingsservices voor uw web-app biedt.</span><span class="sxs-lookup"><span data-stu-id="f4e90-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="f4e90-157">In Hallo **resourcegroep** blade, klikt u op Hallo web app regel.</span><span class="sxs-lookup"><span data-stu-id="f4e90-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Web-app configureren](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="f4e90-159">Hallo blade Web-app klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![site-URL][browse]
4. <span data-ttu-id="f4e90-161">In Hallo WordPress **Welkom** pagina, Voer Hallo configuratie-informatie in die WordPress nodig en klik vervolgens op **WordPress installeren**.</span><span class="sxs-lookup"><span data-stu-id="f4e90-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress configureren](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="f4e90-163">Meld u aan met Hallo-referenties die u hebt gemaakt op Hallo **Welkom** pagina.</span><span class="sxs-lookup"><span data-stu-id="f4e90-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="f4e90-164">De dashboardpagina van uw site wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f4e90-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="f4e90-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4e90-166">Next steps</span></span>
<span data-ttu-id="f4e90-167">U hebt gezien hoe toocreate en implementeren van een PHP-web-app uit de galerie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4e90-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="f4e90-168">Zie voor meer informatie over het gebruik van PHP in Azure Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f4e90-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="f4e90-169">Voor meer informatie over het toowork met App Service Web Apps, Zie Hallo koppelingen op Hallo linkerkant van Hallo pagina (in brede browservensters) of bovenaan Hallo Hallo pagina (in smalle browservensters).</span><span class="sxs-lookup"><span data-stu-id="f4e90-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="f4e90-170">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="f4e90-170">What's changed</span></span>
* <span data-ttu-id="f4e90-171">Zie voor een wijziging van de toohello handleiding van Websites tooApp Service [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f4e90-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
