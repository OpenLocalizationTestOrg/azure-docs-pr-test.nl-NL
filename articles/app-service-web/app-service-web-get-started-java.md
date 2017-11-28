---
title: aaaCreate uw eerste web-app van Java in Azure
description: Meer informatie over hoe toorun web-apps in App Service door het implementeren van een eenvoudige Java-app.
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="ebb06-103">Uw eerste Java-web-app in Azure maken</span><span class="sxs-lookup"><span data-stu-id="ebb06-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="ebb06-104">Hallo [Web-Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) functie van [Azure App Service](../app-service/app-service-value-prop-what-is.md) biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="ebb06-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="ebb06-105">Deze snelstartgids ziet u hoe toodeploy een Java web-app tooApp Service met behulp van Hallo [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="ebb06-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!['Hello Azure'!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="ebb06-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ebb06-108">Prerequisites</span></span>

<span data-ttu-id="ebb06-109">toocomplete deze snelstartgids installeren:</span><span class="sxs-lookup"><span data-stu-id="ebb06-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="ebb06-110">Hallo gratis [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ebb06-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="ebb06-111">Deze Quickstart maakt gebruik van Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="ebb06-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="ebb06-112">Hallo [Azure Toolkit voor Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="ebb06-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="ebb06-113">Een dynamisch webproject maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="ebb06-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="ebb06-114">Selecteer in Eclipse **Bestand** > **Nieuw** > **Dynamisch webproject**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="ebb06-115">In Hallo **nieuwe dynamisch webproject** in het dialoogvenster, naam Hallo project **MyFirstJavaOnAzureWebApp**, en selecteer **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Het dialoogvenster Nieuw dynamisch webproject](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="ebb06-117">Een JSP-pagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="ebb06-117">Add a JSP page</span></span>

<span data-ttu-id="ebb06-118">Geef Projectverkenner weer als dat nu niet het geval is.</span><span class="sxs-lookup"><span data-stu-id="ebb06-118">If Project Explorer is not displayed, restore it.</span></span>

![Java EE-werkruimte voor Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="ebb06-120">Vouw in Projectverkenner Hallo **MyFirstJavaOnAzureWebApp** project.</span><span class="sxs-lookup"><span data-stu-id="ebb06-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="ebb06-121">Klik met de rechtermuisknop op **WebContent** en selecteer vervolgens **Nieuw** > **JSP-bestand**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu voor een nieuw JSP-bestand in Projectverkenner](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="ebb06-123">In Hallo **nieuw JSP-bestand** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="ebb06-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="ebb06-124">Bestand met de Hallo **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="ebb06-125">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-125">Select **Finish**.</span></span>

  ![Het dialoogvenster Nieuw JSP-bestand](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="ebb06-127">In het bestand index.jsp hello, vervangt u Hallo `<body></body>` element met Hallo aantekeningen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb06-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="ebb06-128">Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="ebb06-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="ebb06-129">Hallo web app tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="ebb06-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="ebb06-130">In Projectverkenner met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Azure-Web-App**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Het contextmenu Publiceren als Azure Web App](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="ebb06-132">In Hallo **Azure aanmelden** dialoogvenster, houd Hallo **interactief** optie en selecteer vervolgens **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="ebb06-133">Instructies Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ebb06-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="ebb06-134">Het dialoogvenster Web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="ebb06-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="ebb06-135">Nadat u zich hebt geregistreerd in Azure-account tooyour, Hallo **Web-App implementeren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ebb06-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="ebb06-136">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-136">Select **Create**.</span></span>

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="ebb06-138">Het dialoogvenster App Service maken</span><span class="sxs-lookup"><span data-stu-id="ebb06-138">Create App Service dialog box</span></span>

<span data-ttu-id="ebb06-139">Hallo **Create App Service** dialoogvenster wordt weergegeven met standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="ebb06-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="ebb06-140">aantal Hallo **170602185241** wordt weergegeven in volgende Hallo in het dialoogvenster van uw installatiekopie verschilt.</span><span class="sxs-lookup"><span data-stu-id="ebb06-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="ebb06-142">In Hallo **Create App Service** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="ebb06-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="ebb06-143">Houd naam voor de web-app Hallo Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ebb06-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="ebb06-144">Deze naam moet uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb06-144">This name must be unique across Azure.</span></span> <span data-ttu-id="ebb06-145">Hallo-naam is onderdeel van de URL-adres voor de web-app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebb06-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="ebb06-146">Bijvoorbeeld: als de web-appnaam hello **MyJavaWebApp**, Hallo-URL is *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="ebb06-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="ebb06-147">Houd Hallo standaard webcontainer.</span><span class="sxs-lookup"><span data-stu-id="ebb06-147">Keep hello default web container.</span></span>
* <span data-ttu-id="ebb06-148">Selecteer een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ebb06-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="ebb06-149">Op Hallo **App service-abonnement** tabblad:</span><span class="sxs-lookup"><span data-stu-id="ebb06-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="ebb06-150">**Maken van nieuwe**: gebruik Hallo standaardwaarde Hallo-naam van Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ebb06-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="ebb06-151">**Locatie**: selecteer **West-Europa** of een locatie bij u in de buurt.</span><span class="sxs-lookup"><span data-stu-id="ebb06-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="ebb06-152">**Prijscategorie**: Selecteer Hallo gratis optie.</span><span class="sxs-lookup"><span data-stu-id="ebb06-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="ebb06-153">Voor een functiebeschrijving zie [App Service-prijzen](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ebb06-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="ebb06-155">Het tabblad Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="ebb06-155">Resource group tab</span></span>

<span data-ttu-id="ebb06-156">Selecteer Hallo **resourcegroep** tabblad. Hallo standaard gegenereerde waarde voor de resourcegroep Hallo behouden.</span><span class="sxs-lookup"><span data-stu-id="ebb06-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Het tabblad Resourcegroep](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="ebb06-158">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="ebb06-159">Hello Azure Toolkit Hallo web-app maakt en geeft een dialoogvenster uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebb06-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Het voortgangsvenster voor het maken van een App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="ebb06-161">Het dialoogvenster Web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="ebb06-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="ebb06-162">In Hallo **Web-App implementeren** dialoogvenster, **tooroot implementeren**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="ebb06-163">Als u hebt een app-service op *wingtiptoys.azurewebsites.net* en implementeert u geen toohello root, Hallo web-app met de naam **MyFirstJavaOnAzureWebApp** te wordt geïmplementeerd *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="ebb06-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="ebb06-165">Hallo dialoogvenster vak geeft hello Azure, JDK en web container selecties.</span><span class="sxs-lookup"><span data-stu-id="ebb06-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="ebb06-166">Selecteer **implementeren** tooAzure toopublish Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="ebb06-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="ebb06-167">Wanneer het Hallo-publiceren is voltooid, selecteert u Hallo **gepubliceerde** koppeling in Hallo **Azure Activity Log** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ebb06-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Het dialoogvenster Azure-activiteitenlogboek](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="ebb06-169">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="ebb06-169">Congratulations!</span></span> <span data-ttu-id="ebb06-170">U hebt uw tooAzure web-app is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ebb06-170">You have successfully deployed your web app tooAzure.</span></span> 

!['Hello Azure'!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="ebb06-173">Hallo-web-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="ebb06-173">Update hello web app</span></span>

<span data-ttu-id="ebb06-174">Hallo JSP code tooa verschillende voorbeeldbericht wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ebb06-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="ebb06-175">Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="ebb06-175">Save hello changes.</span></span>

<span data-ttu-id="ebb06-176">In Projectverkenner met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Azure-Web-App**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="ebb06-177">Hallo **Web-App implementeren** in het dialoogvenster wordt weergegeven en toont Hallo-app service die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebb06-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebb06-178">Selecteer **tooroot implementeren** telkens wanneer u publiceert.</span><span class="sxs-lookup"><span data-stu-id="ebb06-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="ebb06-179">Hallo-web-app selecteren en selecteer **implementeren**, die Hallo wijzigingen publiceert.</span><span class="sxs-lookup"><span data-stu-id="ebb06-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="ebb06-180">Wanneer Hallo **Publishing** koppeling wordt weergegeven, selecteert u deze toobrowse toohello web-app en Hallo wijzigingen zien.</span><span class="sxs-lookup"><span data-stu-id="ebb06-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="ebb06-181">Hallo-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="ebb06-181">Manage hello web app</span></span>

<span data-ttu-id="ebb06-182">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toosee Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebb06-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="ebb06-183">Selecteer in het linkermenu Hallo **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="ebb06-183">From hello left menu, select **Resource Groups**.</span></span>

![Navigatie in de portal tooresource groepen](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="ebb06-185">Selecteer Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ebb06-185">Select hello resource group.</span></span> <span data-ttu-id="ebb06-186">Hallo pagina weergegeven Hallo-resources die u hebt gemaakt in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="ebb06-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Resourcegroep myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="ebb06-188">Selecteer Hallo web-app (**webapp 170602193915** in Hallo voorgaande afbeelding).</span><span class="sxs-lookup"><span data-stu-id="ebb06-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="ebb06-189">Hallo **overzicht** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ebb06-189">hello **Overview** page appears.</span></span> <span data-ttu-id="ebb06-190">Deze pagina kunt u een overzicht van hoe Hallo app doet.</span><span class="sxs-lookup"><span data-stu-id="ebb06-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="ebb06-191">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw starten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ebb06-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="ebb06-192">Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuraties die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="ebb06-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![App Service-pagina in Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="ebb06-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebb06-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebb06-195">Aangepast domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="ebb06-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
