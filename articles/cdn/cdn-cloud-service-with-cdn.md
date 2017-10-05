---
title: Een Azure cloudservice integreren met Azure CDN | Microsoft Docs
description: "Informatie over het implementeren van een cloudservice die inhoud van een geïntegreerde Azure CDN-eindpunt"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="a1812-103"><a name="intro"></a>Een cloudservice integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="a1812-104">Een cloudservice kan worden geïntegreerd met Azure CDN, voor de inhoud van de locatie van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="a1812-105">Deze aanpak kunt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a1812-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="a1812-106">Eenvoudig implementeren en bijwerken van installatiekopieën, scripts en stylesheets in mappen van uw cloudservice-project</span><span class="sxs-lookup"><span data-stu-id="a1812-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="a1812-107">De NuGet-pakketten in uw cloudservice, zoals jQuery of Bootstrap versies vervolgens gemakkelijk upgraden</span><span class="sxs-lookup"><span data-stu-id="a1812-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="a1812-108">Beheren van uw webtoepassing en uw CDN-geleverd inhoud alle van de dezelfde Visual Studio-interface</span><span class="sxs-lookup"><span data-stu-id="a1812-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="a1812-109">Uniforme implementatiewerkstroom voor uw webtoepassing en de inhoud van uw CDN-geleverd</span><span class="sxs-lookup"><span data-stu-id="a1812-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="a1812-110">ASP.NET bundeling en minification integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a1812-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a1812-111">What you will learn</span></span>
<span data-ttu-id="a1812-112">In deze zelfstudie leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="a1812-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="a1812-113">Een Azure CDN-eindpunt integreren met de cloudservice en bedienen van statische inhoud in uw webpagina's van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="a1812-114">Cache-instellingen voor statische inhoud configureren in uw cloudservice</span><span class="sxs-lookup"><span data-stu-id="a1812-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="a1812-115">Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="a1812-116">Dienst gebundeld en inhoud via Azure CDN minified behoud het script foutopsporing ervaring in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1812-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="a1812-117">Terugval uw scripts en CSS configureren wanneer uw Azure CDN offline is</span><span class="sxs-lookup"><span data-stu-id="a1812-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="a1812-118">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="a1812-118">What you will build</span></span>
<span data-ttu-id="a1812-119">U implementeert een cloud service-Webrol met behulp van de ASP.NET MVC-sjabloon, code toevoegen om aan te leveren van inhoud vanaf een geïntegreerde Azure CDN, zoals een installatiekopie van een domeincontroller actie resultaten en de standaard JavaScript en CSS-bestanden, en ook het schrijven van code voor het configureren van het mechanisme voor terugval voor bundels geleverd in het geval dat de CDN offline is.</span><span class="sxs-lookup"><span data-stu-id="a1812-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="a1812-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a1812-120">What you will need</span></span>
<span data-ttu-id="a1812-121">Deze zelfstudie gelden de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="a1812-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="a1812-122">Een actieve [Microsoft Azure-account](/account/)</span><span class="sxs-lookup"><span data-stu-id="a1812-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="a1812-123">Visual Studio 2015 met [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="a1812-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="a1812-124">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="a1812-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="a1812-125">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u uitproberen betaalde Azure-services en zelfs nadat ze gebruikt maximaal kun je het account en gebruik gratis Azure-services, zoals Websites.</span><span class="sxs-lookup"><span data-stu-id="a1812-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="a1812-126">U kunt [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1812-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="a1812-127">Een cloudservice implementeren</span><span class="sxs-lookup"><span data-stu-id="a1812-127">Deploy a cloud service</span></span>
<span data-ttu-id="a1812-128">In deze sectie maakt u de standaard ASP.NET MVC-toepassingssjabloon in Visual Studio 2015 implementeren in een cloud service-Webrol, en vervolgens te integreren met een nieuw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="a1812-129">Volg de onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="a1812-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="a1812-130">Maak in Visual Studio 2015 een nieuwe Azure-cloud-service in de menubalk door te gaan naar **bestand > Nieuw > Project > Cloud > Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="a1812-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="a1812-131">Een naam geven en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1812-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="a1812-132">Selecteer **ASP.NET-Webrol** en klik op de  **>**  knop.</span><span class="sxs-lookup"><span data-stu-id="a1812-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="a1812-133">Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="a1812-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="a1812-134">Selecteer **MVC** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1812-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="a1812-135">Nu deze rol Web publiceren met een Azure-cloud-service.</span><span class="sxs-lookup"><span data-stu-id="a1812-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="a1812-136">Met de rechtermuisknop op het cloudserviceproject en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a1812-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="a1812-137">Als u nog niet aangemeld bij Microsoft Azure, klikt u op de **account toevoegen...**  vervolgkeuzelijst en klik op de **account toevoegen** menu-item.</span><span class="sxs-lookup"><span data-stu-id="a1812-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="a1812-138">Aanmelden met het Microsoft-account dat u gebruikt voor het activeren van uw Azure-account in de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="a1812-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="a1812-139">Nadat u bent aangemeld, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a1812-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="a1812-140">Ervan uitgaande dat u een cloud-service of storage-account niet hebt gemaakt, kunt Visual Studio u beide maken.</span><span class="sxs-lookup"><span data-stu-id="a1812-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="a1812-141">In de **Cloudservice maken en de Account** dialoogvenster, typt u de gewenste servicenaam en selecteer de gewenste regio.</span><span class="sxs-lookup"><span data-stu-id="a1812-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="a1812-142">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="a1812-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="a1812-143">Controleer de configuratie in de instellingenpagina publiceren en op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a1812-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="a1812-144">Het publicatieproces voor cloudservices kan lang duren.</span><span class="sxs-lookup"><span data-stu-id="a1812-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="a1812-145">Het inschakelen van Web Deploy voor alle functies optie kan zorgen dat uw cloudservice veel sneller foutopsporing door snelle (maar tijdelijke) updates leveren aan uw Web-rollen.</span><span class="sxs-lookup"><span data-stu-id="a1812-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="a1812-146">Zie voor meer informatie over deze optie [publiceren van een Cloudservice met de Azure-hulpprogramma's](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1812-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="a1812-147">Wanneer de **Microsoft Azure Activity Log** zien is dat publicatiestatus **voltooid**, maakt u een CDN-eindpunt geïntegreerd met deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="a1812-148">Als, na de publicatie, wordt de geïmplementeerde cloudservice een scherm weergegeven, is het waarschijnlijk omdat het gebruik van de cloudservice die u hebt geïmplementeerd een [Gast OS die geen .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="a1812-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="a1812-149">U kunt dit probleem door omzeilen [.NET 4.5.2 als een taak starten implementeren](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a1812-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="a1812-150">Nieuwe CDN-profielen maken</span><span class="sxs-lookup"><span data-stu-id="a1812-150">Create a new CDN profile</span></span>
<span data-ttu-id="a1812-151">Een CDN-profiel is een verzameling van CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="a1812-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="a1812-152">Elk profiel bevat een of meer CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="a1812-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="a1812-153">Mogelijk wilt meerdere profielen gebruiken om de CDN-eindpunten te ordenen op basis van het internetdomein, de webtoepassing of andere criteria.</span><span class="sxs-lookup"><span data-stu-id="a1812-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="a1812-154">Als u al een CDN-profiel dat u wilt gebruiken voor deze zelfstudie hebt, gaat u verder met [een nieuw CDN-eindpunt maken](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="a1812-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="a1812-155">Nieuwe CDN-eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="a1812-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="a1812-156">**Een nieuw CDN-eindpunt voor uw opslagaccount maken**</span><span class="sxs-lookup"><span data-stu-id="a1812-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="a1812-157">In de [Azure Management Portal](https://portal.azure.com), gaat u naar uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="a1812-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="a1812-158">Mogelijk hebt u het profiel in de vorige stap vastgemaakt aan het dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1812-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="a1812-159">Als dit niet het geval is, kunt u het dashboard zoeken door op **Bladeren** en vervolgens **CDN-profielen** te klikken en op het profiel te klikken die u aan het eindpunt wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a1812-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="a1812-160">De blade CDN-profiel wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="a1812-160">The CDN profile blade appears.</span></span>
   
    ![CDN-profiel][cdn-profile-settings]
2. <span data-ttu-id="a1812-162">Klik op de knop **Eindpunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a1812-162">Click the **Add Endpoint** button.</span></span>
   
    ![De knop Eindpunt toevoegen][cdn-new-endpoint-button]
   
    <span data-ttu-id="a1812-164">De blade **Een eindpunt toevoegen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-164">The **Add an endpoint** blade appears.</span></span>
   
    ![De blade Een eindpunt toevoegen][cdn-add-endpoint]
3. <span data-ttu-id="a1812-166">Voer een **naam** voor dit CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="a1812-167">Deze naam wordt gebruikt voor toegang tot uw resources in de cache in het domein `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="a1812-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="a1812-168">In de **oorsprongtype** vervolgkeuzelijst *Cloudservice*.</span><span class="sxs-lookup"><span data-stu-id="a1812-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="a1812-169">In de **de hostnaam van oorsprong** vervolgkeuzelijst, selecteer uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="a1812-170">Laat de standaardwaarden voor **oorsprongpad**, **host-header van oorsprong**, en **Protocol/oorsprong poort**.</span><span class="sxs-lookup"><span data-stu-id="a1812-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="a1812-171">U moet ten minste één protocol (HTTP of HTTPS) opgeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="a1812-172">Klik op de knop **Toevoegen** om het nieuwe eindpunt te maken.</span><span class="sxs-lookup"><span data-stu-id="a1812-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="a1812-173">Zodra het eindpunt is gemaakt, wordt deze weergegeven in een lijst met eindpunten voor het profiel.</span><span class="sxs-lookup"><span data-stu-id="a1812-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="a1812-174">In de lijstweergave kunt u zien welke URL u moet gebruiken voor toegang tot de content in cache en het brondomein.</span><span class="sxs-lookup"><span data-stu-id="a1812-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN-eindpunt][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="a1812-176">Het eindpunt onmiddellijk worden niet beschikbaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="a1812-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="a1812-177">Het kan tot 90 minuten voor de registratie worden doorgegeven via het netwerk CDN duren voordat.</span><span class="sxs-lookup"><span data-stu-id="a1812-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="a1812-178">Gebruikers die proberen de naam van het CDN-domein meteen kan gebruiken wordt totdat de inhoud beschikbaar via de CDN is statuscode 404.</span><span class="sxs-lookup"><span data-stu-id="a1812-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="a1812-179">Het CDN-eindpunt testen</span><span class="sxs-lookup"><span data-stu-id="a1812-179">Test the CDN endpoint</span></span>
<span data-ttu-id="a1812-180">Wanneer de publicatiestatus is **voltooid**, open een browservenster en navigeer naar  **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="a1812-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="a1812-181">In mijn setup is deze URL:</span><span class="sxs-lookup"><span data-stu-id="a1812-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="a1812-182">Dit komt overeen met de volgende bron-URL op het CDN-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="a1812-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="a1812-183">Wanneer u naar navigeert  **http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, afhankelijk van uw browser, wordt u gevraagd om te downloaden of open de bootstrap.css die afkomstig zijn van uw gepubliceerde Web-app.</span><span class="sxs-lookup"><span data-stu-id="a1812-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="a1812-184">U hebt ook toegang tot een openbaar toegankelijke URL zijn op  **http://*&lt;serviceName >*.cloudapp.net/** rechtstreeks vanuit uw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="a1812-185">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a1812-185">For example:</span></span>

* <span data-ttu-id="a1812-186">Een JS-bestand van het pad/script</span><span class="sxs-lookup"><span data-stu-id="a1812-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="a1812-187">Alle bestanden uit de/Content pad</span><span class="sxs-lookup"><span data-stu-id="a1812-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="a1812-188">Elke domeincontroller/actie</span><span class="sxs-lookup"><span data-stu-id="a1812-188">Any controller/action</span></span>
* <span data-ttu-id="a1812-189">Als de queryreeks is ingeschakeld op uw CDN-eindpunt elke URL's met querytekenreeksen</span><span class="sxs-lookup"><span data-stu-id="a1812-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="a1812-190">In feite met de bovenstaande configuratie, kunt u de volledige in de cloud-service hosten  **http://*&lt;cdnName >*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="a1812-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="a1812-191">Als ik ga naar **http://camservice.azureedge.net/**, verschijnt het resultaat van de actie van de startpagina/Index.</span><span class="sxs-lookup"><span data-stu-id="a1812-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="a1812-192">Dit betekent niet, maar het is altijd een goed idee om te dienen als een volledige in de cloud-service via Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="a1812-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="a1812-193">Een CDN met statische leveringsoptimalisatie niet per se versnellen levering van dynamische elementen die niet zijn bedoeld om te worden in de cache, of zeer vaak worden bijgewerkt omdat de CDN van een nieuwe versie van de asset vanaf de oorspronkelijke server heel vaak ophalen moet.</span><span class="sxs-lookup"><span data-stu-id="a1812-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="a1812-194">Voor dit scenario kunt u inschakelen [dynamische Site-versnelling](cdn-dynamic-site-acceleration.md) optimalisatie (DSA) op uw CDN-eindpunt dat gebruikmaakt van verschillende manieren om levering van niet-caching geschikte dynamische activa te versnellen.</span><span class="sxs-lookup"><span data-stu-id="a1812-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="a1812-195">Als u een site met een combinatie van statische en dynamische inhoud hebt, u kunt kiezen om te dienen als uw statische inhoud uit CDN met een statische optimalisatie type (zoals algemene webtoepassingen levering) en voor het uitvoeren van dynamische inhoud rechtstreeks vanaf de bronserver of via een CDN-eindpunt met DSA optimalisatie ingeschakeld per geval.</span><span class="sxs-lookup"><span data-stu-id="a1812-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="a1812-196">Daartoe, hebt u al gezien hoe voor toegang tot afzonderlijke inhoudsbestanden van het CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="a1812-197">Ik wordt beschreven hoe u een specifieke domeincontroller actie via een specifieke CDN-eindpunt in dienst inhoud van de domeincontroller acties via Azure CDN bedienen.</span><span class="sxs-lookup"><span data-stu-id="a1812-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="a1812-198">Het alternatief is om te bepalen welke inhoud voor het uitvoeren van Azure CDN op basis van geval in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="a1812-199">Daartoe, hebt u al gezien hoe voor toegang tot afzonderlijke inhoudsbestanden van het CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="a1812-200">Ik wordt beschreven hoe u een specifieke domeincontroller actie via het CDN-eindpunt in behandeling [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="a1812-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="a1812-201">Cacheopties voor statische bestanden in uw cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="a1812-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="a1812-202">U kunt opgeven hoe u statische inhoud in de cache worden opgeslagen in het CDN-eindpunt wilt met Azure CDN-integratie in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="a1812-203">Open hiervoor *Web.config* van uw rol Web project (bijvoorbeeld WebRole1) en voeg een `<staticContent>` element op de `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="a1812-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="a1812-204">De onderstaande XML configureert u de cache om de 3 dagen vervalt.</span><span class="sxs-lookup"><span data-stu-id="a1812-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="a1812-205">Als u dit doet, ziet alle statische bestanden in uw cloudservice dezelfde regel in uw CDN-cache.</span><span class="sxs-lookup"><span data-stu-id="a1812-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="a1812-206">Voor gedetailleerde controle over de clientcache-instellingen, voegt u een *Web.config* bestand naar een map en uw instellingen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a1812-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="a1812-207">Bijvoorbeeld, Voeg een *Web.config* van het bestand in de *\Content* map en vervang de inhoud met de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="a1812-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="a1812-208">Deze instelling zorgt ervoor dat alle statische bestanden van de *\Content* map mogen worden opgeslagen voor 15 dagen.</span><span class="sxs-lookup"><span data-stu-id="a1812-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="a1812-209">Voor meer informatie over het configureren van de `<clientCache>` element, Zie [clientcache &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="a1812-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="a1812-210">In [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller), ook leest u hoe u de cache-instellingen voor de controller actie resultaten in de cache CDN kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="a1812-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="a1812-211">Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="a1812-212">Wanneer u een cloud service-Webrol met Azure CDN integreert, is het relatief gemakkelijk op te leveren van inhoud van de domeincontroller acties via Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="a1812-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="a1812-213">Anders dan voor uw cloud service rechtstreeks via Azure CDN (uitgelegd hierboven) [Maarten Balliauw](https://twitter.com/maartenballiauw) ziet u hoe u dit doen met een leuk MemeGenerator controller in [korte wachttijden op het web met Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="a1812-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="a1812-214">Ik zal gewoon reproduceer het hier.</span><span class="sxs-lookup"><span data-stu-id="a1812-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="a1812-215">Stel dat in uw cloud service die u wilt memes genereren op basis van de installatiekopie van een jonge Chuck Norris (foto's door [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) zoals deze:</span><span class="sxs-lookup"><span data-stu-id="a1812-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="a1812-216">U hebt een eenvoudige `Index` de meme actie waarmee de klanten om op te geven van de items in de afbeelding wordt gegenereerd zodra ze boeken aan de actie.</span><span class="sxs-lookup"><span data-stu-id="a1812-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="a1812-217">Aangezien het Chuck Norris, kunt u deze pagina om te worden globaal sterk populaire zou verwachten.</span><span class="sxs-lookup"><span data-stu-id="a1812-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="a1812-218">Dit is een goed voorbeeld van voor de semi dynamische inhoud met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="a1812-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="a1812-219">Volg de stappen hierboven om deze actie controller instellen:</span><span class="sxs-lookup"><span data-stu-id="a1812-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="a1812-220">In de *\Controllers* map, maak een nieuw .cs bestand aangeroepen *MemeGeneratorController.cs* en vervang de inhoud door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="a1812-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="a1812-221">Zorg ervoor dat het gemarkeerde gedeelte vervangen door uw CDN-naam.</span><span class="sxs-lookup"><span data-stu-id="a1812-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="a1812-222">Klik met de rechtermuisknop in de standaard `Index()` actie en selecteer **weergave toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a1812-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="a1812-223">Accepteer de onderstaande instellingen en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a1812-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="a1812-224">Open de nieuwe *Views\MemeGenerator\Index.cshtml* en vervang de inhoud door de volgende eenvoudige HTML-code voor het indienen van de items:</span><span class="sxs-lookup"><span data-stu-id="a1812-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="a1812-225">De cloudservice opnieuw publiceren en navigeer naar  **http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** in uw browser.</span><span class="sxs-lookup"><span data-stu-id="a1812-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="a1812-226">Wanneer u de formulierwaarden te verzenden `/MemeGenerator/Index`, wordt de `Index_Post` actiemethode retourneert een koppeling naar de `Show` actiemethode met de bijbehorende invoer-ID.</span><span class="sxs-lookup"><span data-stu-id="a1812-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="a1812-227">Wanneer u de koppeling klikt, kunt u de volgende code bereiken:</span><span class="sxs-lookup"><span data-stu-id="a1812-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="a1812-228">Als uw lokale foutopsporing is gekoppeld, krijgt u de gewone foutopsporing ervaring met een lokale omleiding.</span><span class="sxs-lookup"><span data-stu-id="a1812-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="a1812-229">Als deze wordt uitgevoerd in de cloudservice, wordt naar het omleiden:</span><span class="sxs-lookup"><span data-stu-id="a1812-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="a1812-230">Dit komt overeen met de volgende URL van de oorsprong op uw CDN-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="a1812-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="a1812-231">U kunt de `OutputCacheAttribute` -kenmerk uit voor de `Generate` methode om op te geven hoe het resultaat van de actie moet worden in de cache, die Azure CDN wordt geacht.</span><span class="sxs-lookup"><span data-stu-id="a1812-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="a1812-232">De onderstaande code Geef de vervaldatum van een cache van 1 uur (3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="a1812-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="a1812-233">Evenzo kan u fungeren inhoud van elke domeincontroller actie in uw cloudservice via uw Azure CDN, met de gewenste optie voor het opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="a1812-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="a1812-234">In de volgende sectie wordt ik beschreven hoe u de scripts gebundelde en minified en CSS via Azure CDN bedienen.</span><span class="sxs-lookup"><span data-stu-id="a1812-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="a1812-235">ASP.NET bundeling en minification integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a1812-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="a1812-236">Scripts en CSS stylesheets niet vaak worden gewijzigd en voornaamste kandidaten zijn voor de Azure CDN-cache.</span><span class="sxs-lookup"><span data-stu-id="a1812-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="a1812-237">Voor de hele Webrol via uw Azure CDN is de eenvoudigste manier om bundeling en minification integreren met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="a1812-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="a1812-238">Echter, als u niet wilt mogelijk u dit doet, ik wordt beschreven hoe u om dat te doen terwijl de ervaring van de gewenste ontwikkelaars van ASP.NET bundeling en minification, zoals behouden:</span><span class="sxs-lookup"><span data-stu-id="a1812-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="a1812-239">Goede foutopsporing modus ervaring</span><span class="sxs-lookup"><span data-stu-id="a1812-239">Great debug mode experience</span></span>
* <span data-ttu-id="a1812-240">Gestroomlijnde implementatie</span><span class="sxs-lookup"><span data-stu-id="a1812-240">Streamlined deployment</span></span>
* <span data-ttu-id="a1812-241">Onmiddellijke updates voor clients voor script/CSS versie-upgrades</span><span class="sxs-lookup"><span data-stu-id="a1812-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="a1812-242">Terugval mechanisme als uw CDN-eindpunt is mislukt</span><span class="sxs-lookup"><span data-stu-id="a1812-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="a1812-243">Codewijzigingen minimaliseren</span><span class="sxs-lookup"><span data-stu-id="a1812-243">Minimize code modification</span></span>

<span data-ttu-id="a1812-244">In de **WebRole1** project dat u hebt gemaakt in [integreren van een Azure CDN-eindpunt met uw Azure-website en bedienen van statische inhoud in uw webpagina's van Azure CDN](#deploy)Open *App_Start\BundleConfig.cs* en bekijk de `bundles.Add()` methodeaanroepen.</span><span class="sxs-lookup"><span data-stu-id="a1812-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="a1812-245">De eerste `bundles.Add()` instructie voegt u een script bundel op de virtuele map `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="a1812-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="a1812-246">Open vervolgens *Views\Shared\_Layout.cshtml* om te zien hoe de code script bundel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="a1812-247">U moet de volgende regel code Razor vinden:</span><span class="sxs-lookup"><span data-stu-id="a1812-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="a1812-248">Wanneer deze Razor code wordt uitgevoerd in de Azure-Webrol, verschijnt er een `<script>` tag voor de bundel script vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="a1812-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="a1812-249">Echter, als deze wordt uitgevoerd in Visual Studio door te typen `F5`, geeft deze afzonderlijk elke scriptbestand in de bundel weer (in het geval is slechts één scriptbestand is in de bundel):</span><span class="sxs-lookup"><span data-stu-id="a1812-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="a1812-250">Hiermee kunt u fouten opsporen in de JavaScript-code in uw ontwikkelingsomgeving terwijl gelijktijdige clientverbindingen (bundeling) verminderen en het verbeteren van bestand prestaties (minification) in de productieomgeving downloaden.</span><span class="sxs-lookup"><span data-stu-id="a1812-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="a1812-251">Dit is een uitstekende functie handhaven met Azure CDN-integratie.</span><span class="sxs-lookup"><span data-stu-id="a1812-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="a1812-252">Bovendien, omdat de gerenderde bundel al een automatisch gegenereerde versietekenreeks bevat, u wilt repliceren die functionaliteit zodat de telkens wanneer u uw jQuery-versie via NuGet bijwerkt, deze kan worden bijgewerkt op de client zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="a1812-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="a1812-253">Volg de onderstaande stappen integratie ASP.NET bundeling en minification met uw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="a1812-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="a1812-254">Terug in de *App_Start\BundleConfig.cs*, wijzig de `bundles.Add()` methoden voor het gebruik van een andere [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), die een CDN-adres.</span><span class="sxs-lookup"><span data-stu-id="a1812-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="a1812-255">Om dit te doen, vervang de `RegisterBundles` methodedefinitie met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="a1812-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="a1812-256">Zorg ervoor dat u `<yourCDNName>` met de naam van uw Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="a1812-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="a1812-257">In een gewone woorden die u instelt `bundles.UseCdn = true` en een zorgvuldig ontworpen CDN-URL toegevoegd aan elke bundel.</span><span class="sxs-lookup"><span data-stu-id="a1812-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="a1812-258">Bijvoorbeeld, de eerste constructor in de code:</span><span class="sxs-lookup"><span data-stu-id="a1812-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="a1812-259">is gelijk aan:</span><span class="sxs-lookup"><span data-stu-id="a1812-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="a1812-260">Deze constructor leest ASP.NET bundeling en minification weergeven van afzonderlijke scriptbestanden wanneer foutopsporing lokaal wordt uitgevoerd, maar het opgegeven CDN-adres gebruiken voor toegang tot het script in kwestie.</span><span class="sxs-lookup"><span data-stu-id="a1812-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="a1812-261">Let echter op twee belangrijke kenmerken met deze zorgvuldig ontworpen CDN-URL:</span><span class="sxs-lookup"><span data-stu-id="a1812-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="a1812-262">De bron voor deze URL CDN is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, namelijk daadwerkelijk op de virtuele map van de bundel script in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a1812-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="a1812-263">Aangezien u CDN constructor gebruikt, bevat het CDN-scriptcode voor de bundel niet langer de automatisch gegenereerde versietekenreeks in de gerenderde URL.</span><span class="sxs-lookup"><span data-stu-id="a1812-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="a1812-264">Telkens wanneer de script-bundel is aangepast om af te dwingen een cache ontbreekt bij uw Azure CDN, moet u handmatig een unieke versietekenreeks genereren.</span><span class="sxs-lookup"><span data-stu-id="a1812-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="a1812-265">Deze unieke versietekenreeks moet blijven constant via de levensduur van de implementatie te maximaliseren treffers in cache op uw Azure CDN na de implementatie van de bundel op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="a1812-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="a1812-266">De queryreeks v = < W.X.Y.Z > worden van *Properties\AssemblyInfo.cs* in uw webproject rol.</span><span class="sxs-lookup"><span data-stu-id="a1812-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="a1812-267">U kunt een werkstroom voor de implementatie met de assembly-versie wordt verhoogd telkens wanneer u naar Azure publiceren hebben.</span><span class="sxs-lookup"><span data-stu-id="a1812-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="a1812-268">Of u kunt alleen wijzigen *Properties\AssemblyInfo.cs* in uw project moet worden automatisch de versietekenreeks wordt verhoogd telkens wanneer u bouwt, met het jokerteken ' *'.</span><span class="sxs-lookup"><span data-stu-id="a1812-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="a1812-269">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a1812-269">For example:</span></span>
     
        <span data-ttu-id="a1812-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="a1812-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="a1812-271">Elke andere strategie voor het stroomlijnen van het genereren van een unieke tekenreeks op voor de levensduur van een implementatie wordt hier werken.</span><span class="sxs-lookup"><span data-stu-id="a1812-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="a1812-272">Publiceren van de cloudservice en toegang tot de startpagina.</span><span class="sxs-lookup"><span data-stu-id="a1812-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="a1812-273">De HTML-code voor de pagina weergeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-273">View the HTML code for the page.</span></span> <span data-ttu-id="a1812-274">U moet de CDN-URL weergegeven, met een unieke versietekenreeks telkens wanneer u wijzigingen opnieuw naar de cloudservice publiceren te zien.</span><span class="sxs-lookup"><span data-stu-id="a1812-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="a1812-275">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a1812-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="a1812-276">In Visual Studio fouten opsporen in de cloudservice in Visual Studio door te typen `F5`.,</span><span class="sxs-lookup"><span data-stu-id="a1812-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="a1812-277">De HTML-code voor de pagina weergeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-277">View the HTML code for the page.</span></span> <span data-ttu-id="a1812-278">U ziet nog steeds elke scriptbestand afzonderlijk weergegeven zodat u kunt een consistente foutopsporing optreden in Visual Studio hebben.</span><span class="sxs-lookup"><span data-stu-id="a1812-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="a1812-279">Terugval mechanisme voor CDN-URL 's</span><span class="sxs-lookup"><span data-stu-id="a1812-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="a1812-280">Als uw Azure CDN-eindpunt voor een of andere reden mislukt, wilt u de webpagina worden slim voor toegang tot uw oorsprong webserver als de terugvaloptie voor het laden van JavaScript of Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="a1812-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="a1812-281">Het is ernstige verliezen van installatiekopieën op uw website vanwege CDN niet beschikbaar zijn, maar veel ernstiger cruciaal pagina functionaliteit van uw scripts en stylesheets verliezen.</span><span class="sxs-lookup"><span data-stu-id="a1812-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="a1812-282">De [bundel](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) klasse bevat een eigenschap genaamd [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) waarmee u kunt het terugval mechanisme configureren voor CDN-fout.</span><span class="sxs-lookup"><span data-stu-id="a1812-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="a1812-283">Volg de onderstaande stappen voor het gebruik van deze eigenschap:</span><span class="sxs-lookup"><span data-stu-id="a1812-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="a1812-284">Open in uw webrolproject *App_Start\BundleConfig.cs*, waarin u een CDN-URL toegevoegd in elk [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), en breng de volgende gemarkeerde wijzigingen terugval mechanisme toevoegen aan de standaard bundels:</span><span class="sxs-lookup"><span data-stu-id="a1812-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="a1812-285">Wanneer `CdnFallbackExpression` is niet null script is opgenomen in de HTML-code om te testen of de bundel is geladen en als dat niet het geval is, toegang tot de bundel rechtstreeks vanuit de oorsprong-webserver.</span><span class="sxs-lookup"><span data-stu-id="a1812-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="a1812-286">Deze eigenschap moet worden ingesteld op een JavaScript-expressie die wordt gecontroleerd of de respectieve CDN-bundel correct wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="a1812-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="a1812-287">De expressie die nodig is voor het testen van elke bundel is afhankelijk van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="a1812-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="a1812-288">Voor de standaard bundels bovenstaande:</span><span class="sxs-lookup"><span data-stu-id="a1812-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="a1812-289">`window.jquery`is gedefinieerd in jquery-{version} .js</span><span class="sxs-lookup"><span data-stu-id="a1812-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="a1812-290">`$.validator`is gedefinieerd in jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="a1812-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="a1812-291">`window.Modernizr`is gedefinieerd in modernizer-{version} .js</span><span class="sxs-lookup"><span data-stu-id="a1812-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="a1812-292">`$.fn.modal`is gedefinieerd in bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="a1812-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="a1812-293">U mogelijk opgevallen dat ik niet ingesteld CdnFallbackExpression voor de `~/Cointent/css` bundel.</span><span class="sxs-lookup"><span data-stu-id="a1812-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="a1812-294">Dit is omdat er momenteel een [fout in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) die injects een `<script>` tag voor de alternatieve CSS in plaats van de verwachte `<link>` label.</span><span class="sxs-lookup"><span data-stu-id="a1812-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="a1812-295">Er is echter een goede [stijl bundel terugval](https://github.com/EmberConsultingGroup/StyleBundleFallback) die worden aangeboden door [Ember advies groep](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="a1812-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="a1812-296">Als u wilt de oplossing voor CSS gebruikt, kunt u een nieuw .cs-bestand maken in uw webrolproject *App_Start* map met de naam *StyleBundleExtensions.cs*, en vervang de inhoud ervan met de [code vanuit GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="a1812-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="a1812-297">In *App_Start\StyleFundleExtensions.cs*, geef de naamruimte van de rol van uw Web-naam (bijvoorbeeld **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="a1812-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="a1812-298">Ga terug naar `App_Start\BundleConfig.cs` en wijzigen van de laatste `bundles.Add` instructie met de volgende gemarkeerde code:</span><span class="sxs-lookup"><span data-stu-id="a1812-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="a1812-299">Deze nieuwe uitbreidingsmethode maakt gebruik van de dezelfde idee invoeren van een script in de HTML-code om te controleren van de DOM voor de een overeenkomende klassenaam, regelnaam en regel waarde die is gedefinieerd in het CSS-bundel en vallen terug naar de oorsprong webserver als het mislukt om de overeenkomst te vinden.</span><span class="sxs-lookup"><span data-stu-id="a1812-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="a1812-300">De cloudservice opnieuw publiceren en toegang tot de startpagina.</span><span class="sxs-lookup"><span data-stu-id="a1812-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="a1812-301">De HTML-code voor de pagina weergeven.</span><span class="sxs-lookup"><span data-stu-id="a1812-301">View the HTML code for the page.</span></span> <span data-ttu-id="a1812-302">Zult u geïnjecteerde scripts vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="a1812-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="a1812-303">Houd er rekening mee ingevoegd script voor de CSS-bundel bevat nog steeds de onjuiste restant van de `CdnFallbackExpression` eigenschap in de regel:</span><span class="sxs-lookup"><span data-stu-id="a1812-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="a1812-304">Maar omdat het eerste deel van de || expressie wordt altijd waar retourneren, (op de regel die direct boven), de functie document.write() wordt nooit uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a1812-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="a1812-305">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="a1812-305">More Information</span></span>
* [<span data-ttu-id="a1812-306">Overzicht van het Azure Content Delivery Network (CDN)</span><span class="sxs-lookup"><span data-stu-id="a1812-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="a1812-307">Azure CDN gebruiken</span><span class="sxs-lookup"><span data-stu-id="a1812-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="a1812-308">ASP.NET bundeling en Minification</span><span class="sxs-lookup"><span data-stu-id="a1812-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
