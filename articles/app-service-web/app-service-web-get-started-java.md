---
title: Uw eerste Java-web-app in Azure maken
description: In dit artikel leest u hoe u door het implementeren van een eenvoudige Java-app leert hoe u web-apps uitvoert in App Service.
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="c260d-103">Uw eerste Java-web-app in Azure maken</span><span class="sxs-lookup"><span data-stu-id="c260d-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="c260d-104">De functie [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) van [Azure App Service](../app-service/app-service-value-prop-what-is.md) biedt een zeer schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="c260d-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="c260d-105">In deze Quickstart leert u hoe u een Java-web-app implementeert in App Service met behulp van de [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="c260d-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!['Hello Azure'!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="c260d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c260d-108">Prerequisites</span></span>

<span data-ttu-id="c260d-109">Deze onderdelen moeten zijn geïnstalleerd om deze Quickstart te kunnen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c260d-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="c260d-110">De gratis [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c260d-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="c260d-111">Deze Quickstart maakt gebruik van Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="c260d-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="c260d-112">De [Azure Toolkit voor Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="c260d-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="c260d-113">Een dynamisch webproject maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c260d-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="c260d-114">Selecteer in Eclipse **Bestand** > **Nieuw** > **Dynamisch webproject**.</span><span class="sxs-lookup"><span data-stu-id="c260d-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="c260d-115">Geef het project in het dialoogvenster **Nieuw dynamisch webproject** de naam **MyFirstJavaOnAzureWebApp** en selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c260d-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Het dialoogvenster Nieuw dynamisch webproject](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="c260d-117">Een JSP-pagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="c260d-117">Add a JSP page</span></span>

<span data-ttu-id="c260d-118">Geef Projectverkenner weer als dat nu niet het geval is.</span><span class="sxs-lookup"><span data-stu-id="c260d-118">If Project Explorer is not displayed, restore it.</span></span>

![Java EE-werkruimte voor Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="c260d-120">Vouw in Projectverkenner het project **MyFirstJavaOnAzureWebApp** uit.</span><span class="sxs-lookup"><span data-stu-id="c260d-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="c260d-121">Klik met de rechtermuisknop op **WebContent** en selecteer vervolgens **Nieuw** > **JSP-bestand**.</span><span class="sxs-lookup"><span data-stu-id="c260d-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu voor een nieuw JSP-bestand in Projectverkenner](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="c260d-123">In het dialoogvenster **Nieuw JSP-bestand**:</span><span class="sxs-lookup"><span data-stu-id="c260d-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="c260d-124">Noem het bestand **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="c260d-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="c260d-125">Selecteer **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c260d-125">Select **Finish**.</span></span>

  ![Het dialoogvenster Nieuw JSP-bestand](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="c260d-127">Vervang in het bestand index.jsp het element `<body></body>` door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="c260d-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="c260d-128">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="c260d-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="c260d-129">De web-app publiceren in Azure</span><span class="sxs-lookup"><span data-stu-id="c260d-129">Publish the web app to Azure</span></span>

<span data-ttu-id="c260d-130">Klik in Projectverkenner met de rechtermuisknop op het project en selecteer vervolgens **Azure** > **Publiceren als Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="c260d-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Het contextmenu Publiceren als Azure Web App](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="c260d-132">Laat in het dialoogvenster **Azure-aanmelding** de optie **Interactief** ingeschakeld en selecteer **Aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="c260d-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="c260d-133">Volg de instructies om u aan te melden.</span><span class="sxs-lookup"><span data-stu-id="c260d-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="c260d-134">Het dialoogvenster Web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="c260d-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="c260d-135">Nadat u zich hebt aangemeld bij uw Azure-account, wordt het dialoogvenster **Web-app implementeren** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c260d-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="c260d-136">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c260d-136">Select **Create**.</span></span>

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="c260d-138">Het dialoogvenster App Service maken</span><span class="sxs-lookup"><span data-stu-id="c260d-138">Create App Service dialog box</span></span>

<span data-ttu-id="c260d-139">Het dialoogvenster **App Service** wordt weergegeven met standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="c260d-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="c260d-140">De numerieke waarde **170602185241** in de volgende afbeelding is anders in het dialoogvenster dat u ziet.</span><span class="sxs-lookup"><span data-stu-id="c260d-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="c260d-142">In het dialoogvenster **App Service maken**:</span><span class="sxs-lookup"><span data-stu-id="c260d-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="c260d-143">Gebruik de gegenereerde naam voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="c260d-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="c260d-144">Deze naam moet uniek zijn binnen Azure.</span><span class="sxs-lookup"><span data-stu-id="c260d-144">This name must be unique across Azure.</span></span> <span data-ttu-id="c260d-145">De naam is onderdeel van het URL-adres voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="c260d-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="c260d-146">Als de web-app bijvoorbeeld de naam **MyJavaWebApp** heeft, is de URL *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="c260d-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="c260d-147">Gebruik standaard-webcontainer.</span><span class="sxs-lookup"><span data-stu-id="c260d-147">Keep the default web container.</span></span>
* <span data-ttu-id="c260d-148">Selecteer een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c260d-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="c260d-149">Op het tabblad **App Service-plan**:</span><span class="sxs-lookup"><span data-stu-id="c260d-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="c260d-150">**Nieuwe maken**: gebruik de standaardwaarde, wat de naam van het App Service-plan is.</span><span class="sxs-lookup"><span data-stu-id="c260d-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="c260d-151">**Locatie**: selecteer **West-Europa** of een locatie bij u in de buurt.</span><span class="sxs-lookup"><span data-stu-id="c260d-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="c260d-152">**Prijscategorie**: selecteer een gratis variant.</span><span class="sxs-lookup"><span data-stu-id="c260d-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="c260d-153">Voor een functiebeschrijving zie [App Service-prijzen](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c260d-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="c260d-155">Het tabblad Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="c260d-155">Resource group tab</span></span>

<span data-ttu-id="c260d-156">Selecteer het tabblad **Resourcegroep**. Gebruik de gegenereerde standaardwaarde voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c260d-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Het tabblad Resourcegroep](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="c260d-158">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c260d-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="c260d-159">De web-app wordt gemaakt in Azure Toolkit en de voortgang wordt in een dialoogvenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c260d-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Het voortgangsvenster voor het maken van een App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="c260d-161">Het dialoogvenster Web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="c260d-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="c260d-162">Selecteer **Implementeren in hoofdmap** in het dialoogvenster **Web-app implementeren**.</span><span class="sxs-lookup"><span data-stu-id="c260d-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="c260d-163">Als u een app-service hebt in *wingtiptoys.azurewebsites.net* en u niet in de hoofdmap implementeert, wordt de web-app met de naam **MyFirstJavaOnAzureWebApp** geïmplementeerd in *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="c260d-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="c260d-165">In het dialoogvenster ziet u de selecties voor Azure, JDK en webcontainer.</span><span class="sxs-lookup"><span data-stu-id="c260d-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="c260d-166">Selecteer **Implementeren** om de web-app in Azure te publiceren.</span><span class="sxs-lookup"><span data-stu-id="c260d-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="c260d-167">Als het publiceren is voltooid, selecteert u de koppeling **Gepubliceerd** in het dialoogvenster **Azure-activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="c260d-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Het dialoogvenster Azure-activiteitenlogboek](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="c260d-169">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="c260d-169">Congratulations!</span></span> <span data-ttu-id="c260d-170">De web-app is nu geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="c260d-170">You have successfully deployed your web app to Azure.</span></span> 

!['Hello Azure'!](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="c260d-173">De web-app bijwerken</span><span class="sxs-lookup"><span data-stu-id="c260d-173">Update the web app</span></span>

<span data-ttu-id="c260d-174">Wijzig de tekst van de JSP-voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="c260d-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="c260d-175">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="c260d-175">Save the changes.</span></span>

<span data-ttu-id="c260d-176">Klik in Projectverkenner met de rechtermuisknop op het project en selecteer vervolgens **Azure** > **Publiceren als Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="c260d-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="c260d-177">Het dialoogvenster **Web-app implementeren** wordt geopend, met de app-service die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c260d-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="c260d-178">Selecteer **Implementeren in hoofdmap** telkens wanneer u gaat publiceren.</span><span class="sxs-lookup"><span data-stu-id="c260d-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="c260d-179">Selecteer de web-app en selecteer **Implementeren** om de wijzigingen te publiceren.</span><span class="sxs-lookup"><span data-stu-id="c260d-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="c260d-180">Wanneer de koppeling **Publiceren** wordt weergegeven, selecteert u deze om naar de web-app te bladeren en de wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c260d-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="c260d-181">De web-app beheren</span><span class="sxs-lookup"><span data-stu-id="c260d-181">Manage the web app</span></span>

<span data-ttu-id="c260d-182">Ga naar <a href="https://portal.azure.com" target="_blank">Azure Portal</a> om de web-app te zien die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c260d-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="c260d-183">Selecteer **Resourcegroepen** in het linkermenu.</span><span class="sxs-lookup"><span data-stu-id="c260d-183">From the left menu, select **Resource Groups**.</span></span>

![Portalnavigatie naar resourcegroepen](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="c260d-185">Selecteer de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c260d-185">Select the resource group.</span></span> <span data-ttu-id="c260d-186">De pagina bevat de resources die u in deze Quickstart hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c260d-186">The page shows the resources that you created in this quickstart.</span></span>

![Resourcegroep myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="c260d-188">Selecteer de web-app (**webapp 170602193915** in de voorgaande afbeelding).</span><span class="sxs-lookup"><span data-stu-id="c260d-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="c260d-189">De pagina **Overzicht** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c260d-189">The **Overview** page appears.</span></span> <span data-ttu-id="c260d-190">Deze pagina geeft u een overzicht van hoe de app presteert.</span><span class="sxs-lookup"><span data-stu-id="c260d-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="c260d-191">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw starten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c260d-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="c260d-192">De tabbladen aan de linkerkant van de pagina tonen de verschillende configuraties die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="c260d-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![App Service-pagina in Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="c260d-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c260d-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c260d-195">Aangepast domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="c260d-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
