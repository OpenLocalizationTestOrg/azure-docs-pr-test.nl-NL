---
title: aaaCreate een ASP.NET web-app in Azure | Microsoft Docs
description: Meer informatie over hoe toorun web-apps in Azure App Service door het implementeren van Hallo standaard ASP.NET web-app.
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="025ac-103">Een ASP.NET-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="025ac-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="025ac-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="025ac-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="025ac-105">Deze snelstartgids toont hoe toodeploy uw eerste ASP.NET web-app tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="025ac-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="025ac-106">Als u klaar bent, hebt u een resourcegroep die bestaat uit een App Service-plan en een Azure-web-app met een geïmplementeerde webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="025ac-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="025ac-107">Bekijk de video toosee Hallo deze snelstartgids in actie en voer vervolgens Hallo stappen zelf toopublish uw eerste .NET-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="025ac-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="025ac-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="025ac-108">Prerequisites</span></span>

<span data-ttu-id="025ac-109">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="025ac-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="025ac-110">Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello werkbelastingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="025ac-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="025ac-111">**ASP.NET- en web-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="025ac-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="025ac-112">**Azure-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="025ac-112">**Azure development**</span></span>

    ![ASP.NET- en web-ontwikkeling en Azure-ontwikkeling (onder Web en cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="025ac-114">Een ASP.NET-web-app maken</span><span class="sxs-lookup"><span data-stu-id="025ac-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="025ac-115">Maak in Visual Studio een project door **Bestand > Nieuw > Project** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="025ac-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="025ac-116">In Hallo **nieuw Project** dialoogvenster Selecteer **Visual C# > Web > ASP.NET-webtoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="025ac-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="025ac-117">Naam van de toepassing hello _myFirstAzureWebApp_, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="025ac-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Het dialoogvenster Nieuw project](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="025ac-119">U kunt elk type ASP.NET web app tooAzure implementeren.</span><span class="sxs-lookup"><span data-stu-id="025ac-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="025ac-120">Selecteer voor deze snelstartgids Hallo **MVC** sjabloon, en zorg ervoor dat de verificatie is ingesteld, te**geen verificatie**.</span><span class="sxs-lookup"><span data-stu-id="025ac-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="025ac-121">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="025ac-121">Select **OK**.</span></span>

![Het dialoogvenster Nieuw ASP.NET-project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="025ac-123">Hallo-menu en selecteer **fouten opsporen > starten zonder foutopsporing** toorun Hallo web-app lokaal.</span><span class="sxs-lookup"><span data-stu-id="025ac-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![De app lokaal uitvoeren](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="025ac-125">TooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="025ac-125">Publish tooAzure</span></span>

<span data-ttu-id="025ac-126">In Hallo **Solution Explorer**, klik met de rechtermuisknop Hallo **myFirstAzureWebApp** project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="025ac-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publiceren vanuit Solution Explorer](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="025ac-128">Zorg ervoor dat **Microsoft Azure App Service** is geselecteerd en selecteer dan **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="025ac-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publiceren vanaf de projectoverzichtspagina](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="025ac-130">Hiermee opent u Hallo **Create App Service** dialoogvenster waarmee u alle Hallo nodig Azure-resources toorun Hallo ASP.NET-web-app maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="025ac-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="025ac-131">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="025ac-131">Sign in tooAzure</span></span>

<span data-ttu-id="025ac-132">In Hallo **Create App Service** dialoogvenster Selecteer **account toevoegen**, en meld u aan tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="025ac-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="025ac-133">Als u al bent aangemeld, selecteer Hallo account Hallo met de gewenste abonnement uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="025ac-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="025ac-134">Als u al bent aangemeld, selecteert u **Maken** nog niet.</span><span class="sxs-lookup"><span data-stu-id="025ac-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Meld u aan tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="025ac-136">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="025ac-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="025ac-137">Volgende te**resourcegroep**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="025ac-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="025ac-138">Naam Hallo resourcegroep **myResourceGroup** en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="025ac-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="025ac-139">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="025ac-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="025ac-140">Volgende te**App Service-Plan**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="025ac-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="025ac-141">In Hallo **Configure App Service Plan** dialoogvenster Hallo-instellingen in Hallo schermafbeelding Hallo tabel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="025ac-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Een App Service-plan maken](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="025ac-143">Instelling</span><span class="sxs-lookup"><span data-stu-id="025ac-143">Setting</span></span> | <span data-ttu-id="025ac-144">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="025ac-144">Suggested Value</span></span> | <span data-ttu-id="025ac-145">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="025ac-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="025ac-146">App Service-plan</span><span class="sxs-lookup"><span data-stu-id="025ac-146">App Service Plan</span></span>| <span data-ttu-id="025ac-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="025ac-147">myAppServicePlan</span></span> | <span data-ttu-id="025ac-148">Naam van Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="025ac-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="025ac-149">Locatie</span><span class="sxs-lookup"><span data-stu-id="025ac-149">Location</span></span> | <span data-ttu-id="025ac-150">West-Europa</span><span class="sxs-lookup"><span data-stu-id="025ac-150">West Europe</span></span> | <span data-ttu-id="025ac-151">Hallo datacenter waar Hallo web-app wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="025ac-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="025ac-152">Grootte</span><span class="sxs-lookup"><span data-stu-id="025ac-152">Size</span></span> | <span data-ttu-id="025ac-153">Gratis</span><span class="sxs-lookup"><span data-stu-id="025ac-153">Free</span></span> | <span data-ttu-id="025ac-154">De [prijscategorie](https://azure.microsoft.com/pricing/details/app-service/) bepaalt de hosting-functies.</span><span class="sxs-lookup"><span data-stu-id="025ac-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="025ac-155">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="025ac-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="025ac-156">Maken en publiceren van Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="025ac-156">Create and publish hello web app</span></span>

<span data-ttu-id="025ac-157">In **Web-Appnaam**, typ een unieke app-naam (geldige tekens zijn `a-z`, `0-9`, en `-`), of accepteer Hallo unieke naam voor het automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="025ac-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="025ac-158">Hallo-URL van de web-app Hallo is `http://<app_name>.azurewebsites.net`, waarbij `<app_name>` is de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="025ac-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="025ac-159">Selecteer **maken** toostart hello Azure-resources maken.</span><span class="sxs-lookup"><span data-stu-id="025ac-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Naam van web-app configureren](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="025ac-161">Zodra Hallo wizard is voltooid, het Hallo ASP.NET web app tooAzure publiceert en vervolgens wordt gestart in de standaardbrowser Hallo app Hallo.</span><span class="sxs-lookup"><span data-stu-id="025ac-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Gepubliceerde ASP.NET-web-app in Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="025ac-163">Hallo web-appnaam is opgegeven in Hallo [maken en publiceren van stap](#create-and-publish-the-web-app) wordt gebruikt als de URL-voorvoegsel in Hallo indeling Hallo `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="025ac-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="025ac-164">Gefeliciteerd, uw ASP.NET-web-app wordt live uitgevoerd in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="025ac-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="025ac-165">Update Hallo app en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="025ac-165">Update hello app and redeploy</span></span>

<span data-ttu-id="025ac-166">Van Hallo **Solution Explorer**Open _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="025ac-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="025ac-167">Hallo zoeken `<div class="jumbotron">` HTML code aan de bovenkant Hallo en vervang Hallo volledige element Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="025ac-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="025ac-168">tooredeploy tooAzure, klik met de rechtermuisknop Hallo **myFirstAzureWebApp** project in **Solution Explorer** en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="025ac-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="025ac-169">Pagina publiceren in hello, selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="025ac-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="025ac-170">Als het publiceren is voltooid, Start Visual Studio een browser toohello-URL van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="025ac-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Bijgewerkte ASP.NET-web-app in Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="025ac-172">Hello Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="025ac-172">Manage hello Azure web app</span></span>

<span data-ttu-id="025ac-173">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="025ac-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="025ac-174">Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="025ac-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="025ac-176">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="025ac-176">You see your web app's Overview page.</span></span> <span data-ttu-id="025ac-177">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="025ac-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="025ac-179">Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="025ac-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="025ac-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="025ac-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="025ac-181">ASP.NET met SQL Database</span><span class="sxs-lookup"><span data-stu-id="025ac-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
