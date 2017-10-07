---
title: een Azure line-of-business-app met Azure Active Directory-verificatie aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een ASP.NET MVC line-of-business-app in Azure App Service die wordt geverifieerd met Azure Active Directory
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
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="a8be2-103">Een Azure line-of-business-app maken met Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="a8be2-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="a8be2-104">Dit artikel ziet u hoe toocreate een .NET line-of-business-app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) met Hallo [verificatie / autorisatie](../app-service/app-service-authentication-overview.md) functie.</span><span class="sxs-lookup"><span data-stu-id="a8be2-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="a8be2-105">U ziet ook hoe toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory-gegevens in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="a8be2-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="a8be2-106">Hello Azure Active Directory-tenant waarmee u mag een directory Azure alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="a8be2-107">Of het kan zijn [gesynchroniseerd met uw lokale Active Directory](../active-directory/active-directory-aadconnect.md) toocreate een ervaring voor eenmalige aanmelding voor werknemers die on-premises en externe.</span><span class="sxs-lookup"><span data-stu-id="a8be2-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="a8be2-108">In dit artikel gebruikt Hallo standaarddirectory voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a8be2-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="a8be2-109">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="a8be2-109">What you will build</span></span>
<span data-ttu-id="a8be2-110">Maakt u een eenvoudige regel-of-business maken, lezen, bijwerken, verwijderen (CRUD)-toepassing in App Service Web Apps dat nummers items werken met Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="a8be2-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="a8be2-111">Verificatie van gebruikers met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8be2-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="a8be2-112">Query's Directory: gebruikers en groepen met behulp van [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8be2-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="a8be2-113">Gebruik ASP.NET MVC Hallo *geen verificatie* sjabloon</span><span class="sxs-lookup"><span data-stu-id="a8be2-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="a8be2-114">Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in Azure nodig hebt, raadpleegt u [volgende stap](#next).</span><span class="sxs-lookup"><span data-stu-id="a8be2-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="a8be2-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a8be2-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="a8be2-116">U moet volgen toocomplete Hallo in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="a8be2-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="a8be2-117">Een Azure Active Directory-tenant met gebruikers in verschillende groepen</span><span class="sxs-lookup"><span data-stu-id="a8be2-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="a8be2-118">Machtigingen toocreate toepassingen op Hallo Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="a8be2-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="a8be2-119">Visual Studio 2013 Update 4 of hoger</span><span class="sxs-lookup"><span data-stu-id="a8be2-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="a8be2-120">Azure SDK 2.8.1 of hoger</span><span class="sxs-lookup"><span data-stu-id="a8be2-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="a8be2-121">Maken en implementeren van een web-app tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8be2-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="a8be2-122">Klik in Visual Studio op **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a8be2-123">Selecteer **ASP.NET-webtoepassing**, Geef uw project en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="a8be2-124">Selecteer Hallo **MVC** sjabloon, wijzigt u vervolgens de Hallo verificatie te**geen verificatie**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="a8be2-125">Zorg ervoor dat **Host in Cloud Hallo** is geselecteerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="a8be2-126">In Hallo **Create App Service** dialoogvenster, klikt u op **account toevoegen** (en vervolgens **account toevoegen** Hallo vervolgkeuzelijst) toolog in tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a8be2-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="a8be2-127">Zodra vastgelegd in uw web-app configureren.</span><span class="sxs-lookup"><span data-stu-id="a8be2-127">Once logged in configure your web app.</span></span> <span data-ttu-id="a8be2-128">Een resourcegroep en een nieuwe App Service-abonnement maken door te klikken op Hallo respectieve **nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="a8be2-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="a8be2-129">Klik op **extra Azure-services verkennen** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a8be2-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="a8be2-130">In Hallo **Services** tabblad  **+**  tooadd een SQL-Database voor uw app.</span><span class="sxs-lookup"><span data-stu-id="a8be2-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="a8be2-131">In **SQL-Database configureren**, klikt u op **nieuw** toocreate een exemplaar van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8be2-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="a8be2-132">In **SQL Server configureren**, configureren van uw SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="a8be2-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="a8be2-133">Klik vervolgens op **OK**, **OK**, en **maken** tookick uit Hallo app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="a8be2-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="a8be2-134">In **Azure App Service-activiteit**, kunt u zien wanneer Hallo app is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a8be2-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="a8be2-135">Klik op  **publiceren &lt;* appname*> toothis Web-App nu **, klikt u vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="a8be2-136">Als Visual Studio is voltooid, Open het Hallo app publiceren in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="a8be2-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="a8be2-137">Verificatie- en -toegang configureren</span><span class="sxs-lookup"><span data-stu-id="a8be2-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="a8be2-138">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8be2-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a8be2-139">In het linkermenu hello, klikt u op **App Services** > **&lt;*appname*> ** > **verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="a8be2-140">Azure Active Directory-verificatie inschakelen door te klikken **op** > **Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="a8be2-141">Klik op **opslaan** in de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="a8be2-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="a8be2-142">Zodra Hallo verificatie-instellingen zijn opgeslagen, kunt u proberen opnieuw in de browser Hallo tooyour app navigeren.</span><span class="sxs-lookup"><span data-stu-id="a8be2-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="a8be2-143">De standaardinstellingen voor afdwingen verificatie op de hele app Hallo.</span><span class="sxs-lookup"><span data-stu-id="a8be2-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="a8be2-144">Als u al zijn niet aangemeld, bent u omgeleide tooa aanmeldingsscherm.</span><span class="sxs-lookup"><span data-stu-id="a8be2-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="a8be2-145">Nadat u bent aangemeld, ziet u uw app beveiligd door middel van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a8be2-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="a8be2-146">Vervolgens moet u tooenable access toodirectory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="a8be2-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="a8be2-147">Navigeer toohello [klassieke portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a8be2-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="a8be2-148">In het linkermenu hello, klikt u op **Active Directory** > **standaarddirectory** > **toepassingen**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="a8be2-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="a8be2-149">Dit is hello Azure Active Directory-toepassing die App Service voor u tooenable Hallo autorisatie gemaakt / Authentication-functie.</span><span class="sxs-lookup"><span data-stu-id="a8be2-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="a8be2-150">Klik op **gebruikers** en **groepen** toomake ervoor dat u sommige gebruikers en groepen in Hallo map hebt.</span><span class="sxs-lookup"><span data-stu-id="a8be2-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="a8be2-151">Als dit niet het geval is, is enkele testgebruikers en groepen maken.</span><span class="sxs-lookup"><span data-stu-id="a8be2-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="a8be2-152">Klik op **configureren** tooconfigure deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="a8be2-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="a8be2-153">Schuif omlaag toohello **sleutels** gedeelte en een sleutel toevoegen door te selecteren van een duur.</span><span class="sxs-lookup"><span data-stu-id="a8be2-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="a8be2-154">Klik vervolgens op **gedelegeerde machtigingen** en selecteer **mapgegevens lezen**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="a8be2-155">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="a8be2-156">Wanneer uw instellingen zijn opgeslagen, schuif back-up toohello **sleutels** sectie en klikt u op Hallo **kopie** sleutel van de knop toocopy Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="a8be2-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="a8be2-157">Als u deze pagina nu verlaat, u niet kunt tooaccess deze client sleutel ooit opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a8be2-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="a8be2-158">Vervolgens moet u tooconfigure uw web-app met deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="a8be2-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="a8be2-159">Meld u bij toohello [Azure Resource Explorer](https://resources.azure.com) met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a8be2-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="a8be2-160">Bovenaan Hallo Hallo pagina, klikt u op **lezen/schrijven** toomake wijzigingen in hello Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="a8be2-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="a8be2-161">Hallo zoeken verificatie-instellingen voor uw app zich bevindt op abonnementen >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **providers** > **Microsoft.Web**  >  **sites** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="a8be2-162">Klik op **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="a8be2-163">In Hallo deelvenster bewerken, stelt u Hallo `clientSecret` en `additionalLoginParams` eigenschappen als volgt.</span><span class="sxs-lookup"><span data-stu-id="a8be2-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="a8be2-164">Klik op **plaatsen** op Hallo bovenste toosubmit worden uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="a8be2-165">Nu tootest hebt u Hallo autorisatie token tooaccess hello Azure Active Directory Graph API, gaat u naar  **https://&lt;*appname*>.azurewebsites.net/.auth/me** in uw Browser.</span><span class="sxs-lookup"><span data-stu-id="a8be2-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="a8be2-166">Als u alles correct geconfigureerd, ziet u Hallo `access_token` eigenschap in Hallo JSON-antwoord.</span><span class="sxs-lookup"><span data-stu-id="a8be2-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="a8be2-167">Hallo `~/.auth/me` URL-pad wordt beheerd door App Service-verificatie / autorisatie toogive u alle Hallo informatie over de tooyour geverifieerde sessie.</span><span class="sxs-lookup"><span data-stu-id="a8be2-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="a8be2-168">Zie voor meer informatie [verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8be2-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a8be2-169">Hallo `access_token` heeft een vervalperiode in.</span><span class="sxs-lookup"><span data-stu-id="a8be2-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="a8be2-170">Echter App Service-verificatie / autorisatie biedt vernieuwingsfunctionaliteit token met `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="a8be2-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="a8be2-171">Voor meer informatie over het toouse, Zie [App-Token servicearchief](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="a8be2-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="a8be2-172">Vervolgens dient u iets nuttig met Active directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="a8be2-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="a8be2-173">Line-of-business-functionaliteit tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="a8be2-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="a8be2-174">U maakt nu een eenvoudige CRUD work items vastleggen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="a8be2-175">Hallo ~\Models map, maakt u een klassebestand WorkItem.cs aangeroepen en vervang `public class WorkItem {...}` Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="a8be2-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="a8be2-176">met behulp van System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="a8be2-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="a8be2-177">openbare klasse {werkitem</span><span class="sxs-lookup"><span data-stu-id="a8be2-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="a8be2-178">}</span><span class="sxs-lookup"><span data-stu-id="a8be2-178">}</span></span>
   
     <span data-ttu-id="a8be2-179">openbare enum WorkItemStatus {</span><span class="sxs-lookup"><span data-stu-id="a8be2-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="a8be2-180">}</span><span class="sxs-lookup"><span data-stu-id="a8be2-180">}</span></span>
2. <span data-ttu-id="a8be2-181">De juiste Hallo project toomake uw nieuwe model toegankelijk toohello steigers logica in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8be2-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="a8be2-182">Toevoegen van een nieuw item in de gegenereerde `WorkItemsController` toohello ~\Controllers map (met de rechtermuisknop op **domeincontrollers**, wijst u te**toevoegen**, en selecteer **nieuw gegenereerde item**).</span><span class="sxs-lookup"><span data-stu-id="a8be2-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="a8be2-183">Selecteer **MVC 5 Controller with views, using Entity Framework** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="a8be2-184">Selecteer Hallo model dat u hebt gemaakt, klikt u vervolgens op  **+**  en vervolgens **toevoegen** tooadd een gegevenscontext en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="a8be2-185">Zoek in ~\Views\WorkItems\Create.cshtml (een automatisch gegenereerde artikel), Hallo `Html.BeginForm` Help-methode en Hallo volgende gemarkeerde wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="a8be2-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
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
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="a8be2-186">Houd er rekening mee dat `token` en `tenant` worden gebruikt door Hallo `AadPicker` object toomake Azure Active Directory Graph API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="a8be2-187">U voegt `AadPicker` later.</span><span class="sxs-lookup"><span data-stu-id="a8be2-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="a8be2-188">Net zo goed kunt u krijgen `token` en `tenant` vanaf clientzijde Hallo met `~/.auth/me`, maar dat de aanroep van een extra server zou zijn.</span><span class="sxs-lookup"><span data-stu-id="a8be2-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="a8be2-189">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a8be2-189">For example:</span></span>
   > 
   > <span data-ttu-id="a8be2-190">$.ajax ({dataType: 'json', url: '/.auth/me', succes: functie (gegevens) {var token gegevens [0] = .access_token; var tenant = gegevens [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});</span><span class="sxs-lookup"><span data-stu-id="a8be2-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="a8be2-191">Hallo dezelfde aanpassingen maken met ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="a8be2-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="a8be2-192">Hallo `AadPicker` object is gedefinieerd in een script dat u nodig hebt tooadd tooyour project.</span><span class="sxs-lookup"><span data-stu-id="a8be2-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="a8be2-193">Met de rechtermuisknop op Hallo ~\Scripts map, wijs het te**toevoegen**, en klik op **JavaScript-bestand**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="a8be2-194">Type `AadPickerLibrary` voor Hallo bestandsnaam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="a8be2-195">Hallo-inhoud van kopiëren [hier](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="a8be2-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="a8be2-196">Hallo in Hallo script `AadPicker` object aanroepen [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch voor gebruikers en groepen die overeenkomen met de Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="a8be2-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="a8be2-197">Hallo wordt ook gebruikgemaakt van ~\Scripts\AadPickerLibrary.js [jQuery gebruikersinterface automatisch aanvullen widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="a8be2-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="a8be2-198">U moet dus tooadd jQuery UI tooyour project.</span><span class="sxs-lookup"><span data-stu-id="a8be2-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="a8be2-199">Met de rechtermuisknop op het project in en klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="a8be2-200">Klik op Bladeren, in NuGet Package Manager Hallo, type **jquery-ui** in Hallo zoekbalk en klik op **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="a8be2-201">Klik in het rechterdeelvenster hello, **installeren**, klikt u vervolgens op **OK** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a8be2-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="a8be2-202">Open ~\App_Start\BundleConfig.cs en Hallo volgende gemarkeerde wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="a8be2-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
    
    <span data-ttu-id="a8be2-203">Er zijn meer zodat manieren toomanage JavaScript en CSS-bestanden in uw app.</span><span class="sxs-lookup"><span data-stu-id="a8be2-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="a8be2-204">Echter, ter vereenvoudiging NET gaat u toopiggyback op hello-pakketten die worden geladen met elke weergave.</span><span class="sxs-lookup"><span data-stu-id="a8be2-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="a8be2-205">Ten slotte in ~ \Global.asax, toevoegen van de volgende coderegel in Hallo Hallo `Application_Start()` methode.</span><span class="sxs-lookup"><span data-stu-id="a8be2-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="a8be2-206">`Ctrl`+`.`op elke naming resolutie fout te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="a8be2-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="a8be2-207">U moet deze coderegel omdat Hallo standaard MVC-sjabloon gebruikt <code>[ValidateAntiForgeryToken]</code> decoration op een aantal acties Hallo.</span><span class="sxs-lookup"><span data-stu-id="a8be2-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="a8be2-208">Vervaldatum toohello gedrag beschreven door [Brock Allen](https://twitter.com/BrockLAllen) op [MVC 4, AntiForgeryToken en Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) uw HTTP POST ter voorkoming validatie van tokens kan mislukken omdat:</span><span class="sxs-lookup"><span data-stu-id="a8be2-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="a8be2-209">Azure Active Directory verzendt geen Hallo http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider die wordt standaard door Hallo anti-vervalsingstoken vereist.</span><span class="sxs-lookup"><span data-stu-id="a8be2-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="a8be2-210">Als Azure Active Directory directory gesynchroniseerd met AD FS, verzendt Hallo AD FS vertrouwen standaard geen Hallo http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim, maar u kunt AD FS toosend handmatig configureren Deze claim.</span><span class="sxs-lookup"><span data-stu-id="a8be2-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="a8be2-211">`ClaimTypes.NameIdentifies`Hiermee geeft u de claim Hallo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, die Azure Active Directory levert.</span><span class="sxs-lookup"><span data-stu-id="a8be2-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="a8be2-212">Publiceer nu uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-212">Now, publish your changes.</span></span> <span data-ttu-id="a8be2-213">Met de rechtermuisknop op uw project en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="a8be2-214">Klik op **instellingen**, zorg ervoor dat er is een verbinding tekenreeks tooyour SQL-Database, selecteert u **Database bijwerken** toomake Hallo wijzigingen in het schema voor het model en op **publiceren** .</span><span class="sxs-lookup"><span data-stu-id="a8be2-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="a8be2-215">Navigeer in Hallo browser toohttps: / /&lt;*appname*>.azurewebsites.net/workitems en klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a8be2-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="a8be2-216">Klik in het Hallo **AssignedToName** vak.</span><span class="sxs-lookup"><span data-stu-id="a8be2-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="a8be2-217">U ziet nu gebruikers en groepen van uw Azure Active Directory-tenant in een vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a8be2-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="a8be2-218">Typ toofilter of gebruik Hallo `Up` of `Down` sleutel of klik op tooselect Hallo gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="a8be2-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="a8be2-219">Klik op **maken** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a8be2-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="a8be2-220">Klik vervolgens op **bewerken** op Hallo gemaakt werk Hallo tooobserve item hetzelfde gedrag.</span><span class="sxs-lookup"><span data-stu-id="a8be2-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="a8be2-221">Gefeliciteerd, uitvoert u nu een line-of-business-app in Azure met toegang tot directory!</span><span class="sxs-lookup"><span data-stu-id="a8be2-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="a8be2-222">Er is veel meer dat kunt u doen met Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="a8be2-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="a8be2-223">Zie [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="a8be2-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="a8be2-224">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="a8be2-224">Next Step</span></span>
<span data-ttu-id="a8be2-225">Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in azure nodig hebt, raadpleegt u [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) voor een voorbeeld van hello Azure Active Directory-team.</span><span class="sxs-lookup"><span data-stu-id="a8be2-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="a8be2-226">Hier ziet u hoe tooenable functies voor uw Azure Active Directory-toepassing, en vervolgens het autoriseren van gebruikers met Hallo `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="a8be2-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="a8be2-227">Als uw line-of-business-app moet tooon-premises gegevens toegankelijk zijn, Zie [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8be2-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="a8be2-228">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="a8be2-228">Further resources</span></span>
* [<span data-ttu-id="a8be2-229">Verificatie en autorisatie in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a8be2-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="a8be2-230">Verificatie met de on-premises Active Directory in uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="a8be2-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="a8be2-231">Een line-of-business-app in Azure maken met AD FS-authenticatie</span><span class="sxs-lookup"><span data-stu-id="a8be2-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="a8be2-232">App Service Auth en hello Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="a8be2-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="a8be2-233">Microsoft Azure Active Directory-voorbeelden en documentatie</span><span class="sxs-lookup"><span data-stu-id="a8be2-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="a8be2-234">Azure Active Directory ondersteund Token en claimtypen</span><span class="sxs-lookup"><span data-stu-id="a8be2-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
