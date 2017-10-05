---
title: Een Azure line-of-business-app maken met Azure Active Directory-verificatie | Microsoft Docs
description: Informatie over het maken van een ASP.NET MVC-line-of-business-app in Azure App Service die wordt geverifieerd met Azure Active Directory
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="9543b-103">Een Azure line-of-business-app maken met Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="9543b-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="9543b-104">Dit artikel ziet u het maken van een line-of-business-app voor .NET in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) met behulp van de [verificatie / autorisatie](../app-service/app-service-authentication-overview.md) functie.</span><span class="sxs-lookup"><span data-stu-id="9543b-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="9543b-105">Toont ook het gebruik van de [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) directorygegevens query in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9543b-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="9543b-106">De Azure Active Directory-tenant waarmee u mag een directory Azure alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="9543b-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="9543b-107">Of het kan zijn [gesynchroniseerd met uw lokale Active Directory](../active-directory/active-directory-aadconnect.md) voor het maken van een ervaring voor eenmalige aanmelding voor werknemers die on-premises en extern zijn.</span><span class="sxs-lookup"><span data-stu-id="9543b-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="9543b-108">In dit artikel gebruikt de standaarddirectory voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9543b-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="9543b-109">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="9543b-109">What you will build</span></span>
<span data-ttu-id="9543b-110">Maakt u een eenvoudige regel-of-business maken, lezen, bijwerken, verwijderen (CRUD)-toepassing in App Service Web Apps dat nummers werkitems met de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="9543b-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="9543b-111">Verificatie van gebruikers met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9543b-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="9543b-112">Query's Directory: gebruikers en groepen met behulp van [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="9543b-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="9543b-113">Gebruik de ASP.NET MVC *geen verificatie* sjabloon</span><span class="sxs-lookup"><span data-stu-id="9543b-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="9543b-114">Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in Azure nodig hebt, raadpleegt u [volgende stap](#next).</span><span class="sxs-lookup"><span data-stu-id="9543b-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="9543b-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="9543b-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="9543b-116">U moet het volgende om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="9543b-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="9543b-117">Een Azure Active Directory-tenant met gebruikers in verschillende groepen</span><span class="sxs-lookup"><span data-stu-id="9543b-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="9543b-118">Machtigingen voor het maken van toepassingen op de Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="9543b-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="9543b-119">Visual Studio 2013 Update 4 of hoger</span><span class="sxs-lookup"><span data-stu-id="9543b-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="9543b-120">Azure SDK 2.8.1 of hoger</span><span class="sxs-lookup"><span data-stu-id="9543b-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="9543b-121">Maken en implementeren van een web-app in Azure</span><span class="sxs-lookup"><span data-stu-id="9543b-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="9543b-122">Klik in Visual Studio op **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="9543b-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="9543b-123">Selecteer **ASP.NET-webtoepassing**, Geef uw project en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9543b-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="9543b-124">Selecteer de **MVC** sjabloon, wijzigt u vervolgens de authenticatie voor **geen verificatie**.</span><span class="sxs-lookup"><span data-stu-id="9543b-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="9543b-125">Zorg ervoor dat **Host in de Cloud** is geselecteerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9543b-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="9543b-126">In de **Create App Service** dialoogvenster, klikt u op **account toevoegen** (en vervolgens **account toevoegen** in de vervolgkeuzelijst) zich aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9543b-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="9543b-127">Zodra vastgelegd in uw web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="9543b-127">Once logged in configure your web app.</span></span> <span data-ttu-id="9543b-128">Een resourcegroep en een nieuwe App Service-abonnement maken door te klikken op de respectieve **nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="9543b-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="9543b-129">Klik op **extra Azure-services verkennen** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="9543b-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="9543b-130">In de **Services** tabblad  **+**  toevoegen van een SQL-Database voor uw app.</span><span class="sxs-lookup"><span data-stu-id="9543b-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="9543b-131">In **SQL-Database configureren**, klikt u op **nieuw** voor het maken van een SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9543b-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="9543b-132">In **SQL Server configureren**, configureren van uw SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="9543b-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="9543b-133">Klik vervolgens op **OK**, **OK**, en **maken** Activeer het maken van de app in Azure.</span><span class="sxs-lookup"><span data-stu-id="9543b-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="9543b-134">In **Azure App Service-activiteit**, kunt u zien wanneer de app is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9543b-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="9543b-135">Klik op  **publiceren &lt;* appname*> deze Web-App nu **, klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="9543b-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="9543b-136">Zodra de Visual Studio is voltooid, wordt de app publiceren in de browser geopend.</span><span class="sxs-lookup"><span data-stu-id="9543b-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="9543b-137">Verificatie- en -toegang configureren</span><span class="sxs-lookup"><span data-stu-id="9543b-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="9543b-138">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9543b-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9543b-139">Klik in het menu links op **App Services** > **&lt;*appname*> ** > **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="9543b-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="9543b-140">Azure Active Directory-verificatie inschakelen door te klikken **op** > **Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="9543b-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="9543b-141">Klik op **opslaan** in de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="9543b-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="9543b-142">Als de verificatie-instellingen zijn opgeslagen, probeert u navigeren naar uw app opnieuw in de browser.</span><span class="sxs-lookup"><span data-stu-id="9543b-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="9543b-143">De standaardinstellingen voor verificatie op de hele app worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="9543b-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="9543b-144">Als u al zijn niet aangemeld, wordt u omgeleid naar een aanmeldingsscherm.</span><span class="sxs-lookup"><span data-stu-id="9543b-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="9543b-145">Nadat u bent aangemeld, ziet u uw app beveiligd door middel van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9543b-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="9543b-146">Vervolgens moet u toegang tot Active directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="9543b-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="9543b-147">Navigeer naar de [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9543b-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="9543b-148">Klik in het menu links op **Active Directory** > **standaarddirectory** > **toepassingen** > **&lt;*appname*> **.</span><span class="sxs-lookup"><span data-stu-id="9543b-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="9543b-149">Dit is de Azure Active Directory-toepassing die App Service voor u gemaakt waarmee de autorisatie / Authentication-functie.</span><span class="sxs-lookup"><span data-stu-id="9543b-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="9543b-150">Klik op **gebruikers** en **groepen** om ervoor te zorgen dat u sommige gebruikers en groepen in de map hebt.</span><span class="sxs-lookup"><span data-stu-id="9543b-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="9543b-151">Als dit niet het geval is, is enkele testgebruikers en groepen maken.</span><span class="sxs-lookup"><span data-stu-id="9543b-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="9543b-152">Klik op **configureren** om deze toepassing te configureren.</span><span class="sxs-lookup"><span data-stu-id="9543b-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="9543b-153">Schuif omlaag naar de **sleutels** gedeelte en een sleutel toevoegen door te selecteren van een duur.</span><span class="sxs-lookup"><span data-stu-id="9543b-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="9543b-154">Klik vervolgens op **gedelegeerde machtigingen** en selecteer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="9543b-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="9543b-155">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9543b-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="9543b-156">Wanneer uw instellingen zijn opgeslagen, schuif terug tot de **sleutels** sectie en klik op de **kopie** knop om te kopiëren van de sleutel van de client.</span><span class="sxs-lookup"><span data-stu-id="9543b-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="9543b-157">Als u deze pagina nu verlaat, kunt u niet de sleutel van deze client ooit opnieuw toegang tot.</span><span class="sxs-lookup"><span data-stu-id="9543b-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="9543b-158">Vervolgens moet u uw web-app configureren met deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="9543b-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="9543b-159">Meld u aan bij de [Azure Resource Explorer](https://resources.azure.com) met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9543b-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="9543b-160">Klik boven aan de pagina op **lezen/schrijven** wijzigingen aanbrengen in de Azure Resourceverkenner.</span><span class="sxs-lookup"><span data-stu-id="9543b-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="9543b-161">De verificatie-instellingen voor uw app zich bevindt op abonnementen vinden >  **&lt;* subscriptionname*> ** > **resourceGroups** > **&lt;*resourcegroupname*> ** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*> ** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="9543b-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="9543b-162">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="9543b-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="9543b-163">Stel in het deelvenster bewerken de `clientSecret` en `additionalLoginParams` eigenschappen als volgt.</span><span class="sxs-lookup"><span data-stu-id="9543b-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="9543b-164">Klik op **plaatsen** boven uw wijzigingen wilt indienen.</span><span class="sxs-lookup"><span data-stu-id="9543b-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="9543b-165">Als u wilt testen als u het verificatietoken voor toegang tot Azure Active Directory Graph API hebt, navigeer nu naar  **https://&lt;*appname*>.azurewebsites.net/.auth/me** in uw browser.</span><span class="sxs-lookup"><span data-stu-id="9543b-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="9543b-166">Als u alles correct geconfigureerd, ziet u de `access_token` eigenschap in het JSON-antwoord.</span><span class="sxs-lookup"><span data-stu-id="9543b-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="9543b-167">De `~/.auth/me` URL-pad wordt beheerd door App Service-verificatie / autorisatie zodat u alle informatie die betrekking hebben op uw geverifieerde sessie.</span><span class="sxs-lookup"><span data-stu-id="9543b-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="9543b-168">Zie voor meer informatie [verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9543b-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9543b-169">De `access_token` heeft een vervalperiode in.</span><span class="sxs-lookup"><span data-stu-id="9543b-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="9543b-170">Echter App Service-verificatie / autorisatie biedt vernieuwingsfunctionaliteit token met `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="9543b-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="9543b-171">Zie voor meer informatie over het gebruik ervan [App-Token servicearchief](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="9543b-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="9543b-172">Vervolgens dient u iets nuttig met Active directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="9543b-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="9543b-173">Line-of-business-functionaliteit toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="9543b-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="9543b-174">U maakt nu een eenvoudige CRUD work items vastleggen.</span><span class="sxs-lookup"><span data-stu-id="9543b-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="9543b-175">Maak een klassebestand WorkItem.cs aangeroepen in de map ~\Models en vervang `public class WorkItem {...}` met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="9543b-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="9543b-176">met behulp van System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="9543b-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="9543b-177">openbare klasse {werkitem</span><span class="sxs-lookup"><span data-stu-id="9543b-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="9543b-178">}</span><span class="sxs-lookup"><span data-stu-id="9543b-178">}</span></span>
   
     <span data-ttu-id="9543b-179">openbare enum WorkItemStatus {</span><span class="sxs-lookup"><span data-stu-id="9543b-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="9543b-180">}</span><span class="sxs-lookup"><span data-stu-id="9543b-180">}</span></span>
2. <span data-ttu-id="9543b-181">Bouw het project voor het nieuwe model toegankelijk maken voor de logica steigers in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9543b-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="9543b-182">Voeg een nieuw item in de gegenereerde `WorkItemsController` naar de map ~\Controllers (met de rechtermuisknop op **domeincontrollers**, wijs **toevoegen**, en selecteer **nieuw gegenereerde item**).</span><span class="sxs-lookup"><span data-stu-id="9543b-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="9543b-183">Selecteer **MVC 5 Controller with views, using Entity Framework** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9543b-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="9543b-184">Selecteer het model dat u gemaakt en klik vervolgens op  **+**  en vervolgens **toevoegen** een gegevenscontext toevoegen en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9543b-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="9543b-185">Zoek in ~\Views\WorkItems\Create.cshtml (een automatisch gegenereerde artikel), de `Html.BeginForm` Help-methode en de volgende gemarkeerde wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="9543b-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="9543b-186">Houd er rekening mee dat `token` en `tenant` worden gebruikt door de `AadPicker` object Azure Active Directory Graph API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9543b-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="9543b-187">U voegt `AadPicker` later.</span><span class="sxs-lookup"><span data-stu-id="9543b-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="9543b-188">U krijgt net zo goed `token` en `tenant` vanaf de client met `~/.auth/me`, maar dat zou de aanroep van een extra server.</span><span class="sxs-lookup"><span data-stu-id="9543b-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="9543b-189">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9543b-189">For example:</span></span>
   > 
   > <span data-ttu-id="9543b-190">$.ajax ({dataType: 'json', url: '/.auth/me', succes: functie (gegevens) {var token gegevens [0] = .access_token; var tenant = gegevens [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});</span><span class="sxs-lookup"><span data-stu-id="9543b-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="9543b-191">Met dezelfde wijzigingen aanbrengen ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="9543b-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="9543b-192">De `AadPicker` -object is gedefinieerd in een script dat u wilt toevoegen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="9543b-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="9543b-193">Met de rechtermuisknop op de map ~\Scripts, wijst u **toevoegen**, en klik op **JavaScript-bestand**.</span><span class="sxs-lookup"><span data-stu-id="9543b-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="9543b-194">Type `AadPickerLibrary` voor de bestandsnaam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9543b-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="9543b-195">Kopieer de inhoud van [hier](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="9543b-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="9543b-196">In het script wordt de `AadPicker` object aanroepen [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) om te zoeken naar gebruikers en groepen die overeenkomen met de invoer.</span><span class="sxs-lookup"><span data-stu-id="9543b-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="9543b-197">~\Scripts\AadPickerLibrary.js gebruikt ook de [jQuery gebruikersinterface automatisch aanvullen widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="9543b-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="9543b-198">U moet dus jQuery UI toevoegen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="9543b-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="9543b-199">Met de rechtermuisknop op het project in en klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="9543b-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="9543b-200">In de NuGet Package Manager, klikt u op Bladeren, type **jquery-ui** in de zoekbalk en op **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="9543b-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="9543b-201">Klik in het rechterdeelvenster **installeren**, klikt u vervolgens op **OK** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="9543b-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="9543b-202">Open ~\App_Start\BundleConfig.cs en de volgende gemarkeerde wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="9543b-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="9543b-203">Er zijn meer zodat manieren voor het beheren van JavaScript en CSS-bestanden in uw app.</span><span class="sxs-lookup"><span data-stu-id="9543b-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="9543b-204">Echter voor eenvoud gaat net u op de pakketten die worden geladen met elke weergave worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9543b-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="9543b-205">Ten slotte in ~ \Global.asax, voeg de volgende regel code in de `Application_Start()` methode.</span><span class="sxs-lookup"><span data-stu-id="9543b-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="9543b-206">`Ctrl`+`.`op elke naming omzettingsfout om dit te herstellen.</span><span class="sxs-lookup"><span data-stu-id="9543b-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="9543b-207">U moet deze coderegel omdat de standaard MVC-sjabloon gebruikt <code>[ValidateAntiForgeryToken]</code> decoration op enkele van de acties.</span><span class="sxs-lookup"><span data-stu-id="9543b-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="9543b-208">Als gevolg van het gedrag beschreven door [Brock Allen](https://twitter.com/BrockLAllen) op [MVC 4, AntiForgeryToken en Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) uw HTTP POST ter voorkoming validatie van tokens kan mislukken omdat:</span><span class="sxs-lookup"><span data-stu-id="9543b-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="9543b-209">Azure Active Directory verzendt de http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider die wordt standaard door de anti-vervalsingstoken vereist.</span><span class="sxs-lookup"><span data-stu-id="9543b-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="9543b-210">Als Azure Active Directory directory gesynchroniseerd met AD FS, verzendt de vertrouwensrelatie van de AD FS standaard de claim http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, maar u kunt AD FS voor het verzenden van deze claim handmatig configureren.</span><span class="sxs-lookup"><span data-stu-id="9543b-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="9543b-211">`ClaimTypes.NameIdentifies`Hiermee geeft u de claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, die Azure Active Directory levert.</span><span class="sxs-lookup"><span data-stu-id="9543b-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="9543b-212">Publiceer nu uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="9543b-212">Now, publish your changes.</span></span> <span data-ttu-id="9543b-213">Met de rechtermuisknop op uw project en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="9543b-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="9543b-214">Klik op **instellingen**, zorg ervoor dat er een verbindingsreeks voor de SQL-Database, selecteert u **Database bijwerken** om u aan te maken van de wijzigingen in het schema voor het model, klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="9543b-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="9543b-215">Navigeer in de browser naar https://&lt;*appname*>.azurewebsites.net/workitems en klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="9543b-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="9543b-216">Klik in de **AssignedToName** vak.</span><span class="sxs-lookup"><span data-stu-id="9543b-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="9543b-217">U ziet nu gebruikers en groepen van uw Azure Active Directory-tenant in een vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9543b-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="9543b-218">Typ om te filteren of gebruik de `Up` of `Down` sleutel of schakelt u de gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="9543b-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="9543b-219">Klik op **maken** de wijzigingen wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="9543b-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="9543b-220">Klik vervolgens op **bewerken** op het gemaakte werkitem hetzelfde gedrag in acht nemen.</span><span class="sxs-lookup"><span data-stu-id="9543b-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="9543b-221">Gefeliciteerd, uitvoert u nu een line-of-business-app in Azure met toegang tot directory!</span><span class="sxs-lookup"><span data-stu-id="9543b-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="9543b-222">Er is veel meer dat kunt u doen met de Graph API.</span><span class="sxs-lookup"><span data-stu-id="9543b-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="9543b-223">Zie [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="9543b-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="9543b-224">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="9543b-224">Next Step</span></span>
<span data-ttu-id="9543b-225">Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in azure nodig hebt, raadpleegt u [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) voor een voorbeeld van het team van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9543b-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="9543b-226">Hier ziet u het inschakelen van functies voor uw Azure Active Directory-toepassing en vervolgens het autoriseren van gebruikers met de `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="9543b-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="9543b-227">Als uw line-of-business-app toegang tot on-premises gegevens moet, Zie [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9543b-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="9543b-228">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="9543b-228">Further resources</span></span>
* [<span data-ttu-id="9543b-229">Verificatie en autorisatie in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9543b-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="9543b-230">Verificatie met de on-premises Active Directory in uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="9543b-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="9543b-231">Een line-of-business-app in Azure maken met AD FS-authenticatie</span><span class="sxs-lookup"><span data-stu-id="9543b-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="9543b-232">App Service-verificatie en Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="9543b-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="9543b-233">Microsoft Azure Active Directory-voorbeelden en documentatie</span><span class="sxs-lookup"><span data-stu-id="9543b-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="9543b-234">Azure Active Directory ondersteund Token en claimtypen</span><span class="sxs-lookup"><span data-stu-id="9543b-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
