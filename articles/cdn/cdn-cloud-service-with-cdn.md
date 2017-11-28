---
title: een cloudservice van Azure met Azure CDN aaaIntegrate | Microsoft Docs
description: "Meer informatie over hoe toodeploy een cloudservice die fungeert inhoud van een geïntegreerde Azure CDN-eindpunt"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="4be9a-103"><a name="intro"></a>Een cloudservice integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="4be9a-104">Een cloudservice kan worden geïntegreerd met Azure CDN, voor de inhoud van Hallo cloudservice-locatie.</span><span class="sxs-lookup"><span data-stu-id="4be9a-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="4be9a-105">Deze aanpak geeft u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="4be9a-106">Eenvoudig implementeren en bijwerken van installatiekopieën, scripts en stylesheets in mappen van uw cloudservice-project</span><span class="sxs-lookup"><span data-stu-id="4be9a-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="4be9a-107">Hallo NuGet-pakketten in uw cloudservice, zoals jQuery of Bootstrap versies vervolgens gemakkelijk upgraden</span><span class="sxs-lookup"><span data-stu-id="4be9a-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="4be9a-108">Beheren van uw webtoepassing en uw CDN-aangeboden inhoud vanaf Hallo dezelfde Visual Studio-interface</span><span class="sxs-lookup"><span data-stu-id="4be9a-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="4be9a-109">Uniforme implementatiewerkstroom voor uw webtoepassing en de inhoud van uw CDN-geleverd</span><span class="sxs-lookup"><span data-stu-id="4be9a-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="4be9a-110">ASP.NET bundeling en minification integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4be9a-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4be9a-111">What you will learn</span></span>
<span data-ttu-id="4be9a-112">In deze zelfstudie leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="4be9a-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="4be9a-113">Een Azure CDN-eindpunt integreren met de cloudservice en bedienen van statische inhoud in uw webpagina's van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="4be9a-114">Cache-instellingen voor statische inhoud configureren in uw cloudservice</span><span class="sxs-lookup"><span data-stu-id="4be9a-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="4be9a-115">Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="4be9a-116">Dienst gebundeld en inhoud via Azure CDN minified behoud Hallo script foutopsporing ervaring in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4be9a-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="4be9a-117">Terugval uw scripts en CSS configureren wanneer uw Azure CDN offline is</span><span class="sxs-lookup"><span data-stu-id="4be9a-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="4be9a-118">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="4be9a-118">What you will build</span></span>
<span data-ttu-id="4be9a-119">U implementeert een cloud service-Webrol Hallo standaard-ASP.NET MVC-sjabloon gebruikt, voegt u code tooserve inhoud van een geïntegreerde Azure CDN, zoals een installatiekopie van een domeincontroller actie resultaten en Hallo standaard JavaScript en CSS-bestanden, en ook schrijven code tooconfigure Hallo terugval mechanisme voor bundels geleverd in Hallo gebeurtenis die Hallo CDN is offline.</span><span class="sxs-lookup"><span data-stu-id="4be9a-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="4be9a-120">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="4be9a-120">What you will need</span></span>
<span data-ttu-id="4be9a-121">Deze zelfstudie heeft Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="4be9a-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="4be9a-122">Een actieve [Microsoft Azure-account](/account/)</span><span class="sxs-lookup"><span data-stu-id="4be9a-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="4be9a-123">Visual Studio 2015 met [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="4be9a-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="4be9a-124">U moet een Azure-account toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="4be9a-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="4be9a-125">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze allemaal hebt gebruikt kunt u maximaal Hallo account houden en gebruik gratis Azure-services, zoals Websites.</span><span class="sxs-lookup"><span data-stu-id="4be9a-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="4be9a-126">U kunt [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4be9a-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="4be9a-127">Een cloudservice implementeren</span><span class="sxs-lookup"><span data-stu-id="4be9a-127">Deploy a cloud service</span></span>
<span data-ttu-id="4be9a-128">In deze sectie wordt u Hallo standaard ASP.NET MVC-toepassingssjabloon in Visual Studio 2015 tooa cloud service-Webrol implementeren en vervolgens te integreren met een nieuw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="4be9a-129">Volg onderstaande Hallo instructies:</span><span class="sxs-lookup"><span data-stu-id="4be9a-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="4be9a-130">In Visual Studio 2015, moet u een nieuwe Azure-cloud-service in de menubalk Hallo maken te gaan**bestand > Nieuw > Project > Cloud > Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="4be9a-131">Een naam geven en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="4be9a-132">Selecteer **ASP.NET-Webrol** en klik op Hallo  **>**  knop.</span><span class="sxs-lookup"><span data-stu-id="4be9a-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="4be9a-133">Klik op OK.</span><span class="sxs-lookup"><span data-stu-id="4be9a-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="4be9a-134">Selecteer **MVC** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="4be9a-135">Publiceer nu deze Web-rol tooan Azure-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4be9a-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="4be9a-136">Hallo-cloudserviceproject met de rechtermuisknop en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="4be9a-137">Als u nog niet aangemeld bij Microsoft Azure, klikt u op Hallo **account toevoegen...**  vervolgkeuzelijst en klik op Hallo **account toevoegen** menu-item.</span><span class="sxs-lookup"><span data-stu-id="4be9a-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="4be9a-138">In het Hallo-aanmeldingspagina, zich aanmelden met Hallo Microsoft-account die u gebruikt tooactivate uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4be9a-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="4be9a-139">Nadat u bent aangemeld, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="4be9a-140">Ervan uitgaande dat u een cloud-service of storage-account niet hebt gemaakt, kunt Visual Studio u beide maken.</span><span class="sxs-lookup"><span data-stu-id="4be9a-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="4be9a-141">In Hallo **Cloudservice maken en de Account** dialoogvenster, type Hallo gewenste servicenaam en selecteer Hallo gewenste regio.</span><span class="sxs-lookup"><span data-stu-id="4be9a-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="4be9a-142">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="4be9a-143">In Hallo instellingenpagina publiceren, Hallo-configuratie controleren en klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="4be9a-144">Hallo publicatieproces voor cloudservices kan lang duren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="4be9a-145">Hallo Web Deploy inschakelen voor alle functies optie kan zorgen dat uw cloudservice veel sneller door snelle (maar tijdelijke) updates tooyour webrollen foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="4be9a-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="4be9a-146">Zie voor meer informatie over deze optie [publiceren van een Cloudservice met behulp van hulpprogramma's van Azure Hallo](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="4be9a-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="4be9a-147">Wanneer Hallo **Microsoft Azure Activity Log** zien is dat publicatiestatus **voltooid**, maakt u een CDN-eindpunt geïntegreerd met deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4be9a-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="4be9a-148">Als, Hallo geïmplementeerd cloudservice weergegeven na de publicatie, een foutscherm, is het waarschijnlijk omdat het Hallo-cloudservice die u hebt geïmplementeerd een [Gast OS die geen .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="4be9a-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="4be9a-149">U kunt dit probleem door omzeilen [.NET 4.5.2 als een taak starten implementeren](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4be9a-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="4be9a-150">Nieuwe CDN-profielen maken</span><span class="sxs-lookup"><span data-stu-id="4be9a-150">Create a new CDN profile</span></span>
<span data-ttu-id="4be9a-151">Een CDN-profiel is een verzameling van CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="4be9a-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="4be9a-152">Elk profiel bevat een of meer CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="4be9a-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="4be9a-153">U kunt desgewenst toouse meerdere profielen tooorganize uw CDN-eindpunten door internetdomein, webtoepassing of andere criteria.</span><span class="sxs-lookup"><span data-stu-id="4be9a-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="4be9a-154">Als u al een CDN-profiel wilt u toouse voor deze zelfstudie hebt, gaat u verder te[een nieuw CDN-eindpunt maken](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="4be9a-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="4be9a-155">Nieuwe CDN-eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="4be9a-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="4be9a-156">**een nieuw CDN-eindpunt voor uw opslagaccount toocreate**</span><span class="sxs-lookup"><span data-stu-id="4be9a-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="4be9a-157">In Hallo [Azure Management Portal](https://portal.azure.com), navigeer tooyour CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="4be9a-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="4be9a-158">U kunt hebt vastgemaakt toohello dashboard in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be9a-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="4be9a-159">Als u niet, u kunt vinden door te klikken op **Bladeren**, klikt u vervolgens **CDN-profielen**, en te klikken op Hallo profiel u van plan bent tooadd het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="4be9a-160">blade Hallo CDN-profiel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-160">hello CDN profile blade appears.</span></span>
   
    ![CDN-profiel][cdn-profile-settings]
2. <span data-ttu-id="4be9a-162">Klik op Hallo **eindpunt toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4be9a-162">Click hello **Add Endpoint** button.</span></span>
   
    ![De knop Eindpunt toevoegen][cdn-new-endpoint-button]
   
    <span data-ttu-id="4be9a-164">Hallo **een eindpunt toevoegen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![De blade Een eindpunt toevoegen][cdn-add-endpoint]
3. <span data-ttu-id="4be9a-166">Voer een **naam** voor dit CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="4be9a-167">Deze naam worden uw resources in de cache op Hallo domein gebruikte tooaccess `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="4be9a-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="4be9a-168">In Hallo **oorsprongtype** vervolgkeuzelijst *Cloudservice*.</span><span class="sxs-lookup"><span data-stu-id="4be9a-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="4be9a-169">In Hallo **de hostnaam van oorsprong** vervolgkeuzelijst, selecteer uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4be9a-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="4be9a-170">Laat de standaardwaarden voor Hallo **oorsprongpad**, **host-header van oorsprong**, en **Protocol/oorsprong poort**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="4be9a-171">U moet ten minste één protocol (HTTP of HTTPS) opgeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="4be9a-172">Klik op Hallo **toevoegen** knop toocreate Hallo nieuw eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="4be9a-173">Zodra het Hallo-eindpunt is gemaakt, wordt deze weergegeven in een lijst met eindpunten voor Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="4be9a-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="4be9a-174">Hallo lijstweergave kunt u zien Hallo URL toouse tooaccess in de cache opgeslagen inhoud, evenals Hallo brondomein.</span><span class="sxs-lookup"><span data-stu-id="4be9a-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![CDN-eindpunt][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="4be9a-176">Hallo-eindpunt onmiddellijk worden niet beschikbaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="4be9a-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="4be9a-177">Hallo registratie toopropagate via Hallo CDN netwerk too90 minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="4be9a-178">Totdat het Hallo-inhoud is beschikbaar via Hallo CDN, kunnen gebruikers die direct toouse Hallo CDN-domeinnaam proberen statuscode 404 ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="4be9a-179">Test Hallo CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="4be9a-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="4be9a-180">Wanneer Hallo publicatiestatus is **voltooid**, open een browservenster en navigeer te**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="4be9a-181">In mijn setup is deze URL:</span><span class="sxs-lookup"><span data-stu-id="4be9a-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="4be9a-182">Dat overeenkomt met toohello oorsprong URL bij Hallo CDN-eindpunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="4be9a-183">Wanneer u navigeert te**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, afhankelijk van uw browser, kunt u zich na vragen aan gebruiker toodownload of open Hallo bootstrap.css die afkomstig zijn van uw gepubliceerde Web-app.</span><span class="sxs-lookup"><span data-stu-id="4be9a-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="4be9a-184">U hebt ook toegang tot een openbaar toegankelijke URL zijn op  **http://*&lt;serviceName >*.cloudapp.net/** rechtstreeks vanuit uw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="4be9a-185">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4be9a-185">For example:</span></span>

* <span data-ttu-id="4be9a-186">Een bestand .js van Hallo/script-pad</span><span class="sxs-lookup"><span data-stu-id="4be9a-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="4be9a-187">Alle inhoud bestanden Hallo/Content pad</span><span class="sxs-lookup"><span data-stu-id="4be9a-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="4be9a-188">Elke domeincontroller/actie</span><span class="sxs-lookup"><span data-stu-id="4be9a-188">Any controller/action</span></span>
* <span data-ttu-id="4be9a-189">Als de queryreeks Hallo is ingeschakeld op uw CDN-eindpunt elke URL's met querytekenreeksen</span><span class="sxs-lookup"><span data-stu-id="4be9a-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="4be9a-190">Met Hallo bovenstaande configuratie, kunt u in feite Hallo volledige in de cloud-service hosten  **http://*&lt;cdnName >*.azureedge.net/**. Als ik te navigeren**http://camservice.azureedge.net/ ** verschijnt Hallo actie resultaat van de startpagina/Index.</span><span class="sxs-lookup"><span data-stu-id="4be9a-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="4be9a-191">Dit betekent niet, maar het is altijd een goed idee tooserve een volledige in de cloud-service via Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="4be9a-192">Een CDN met statische leveringsoptimalisatie niet per se versnellen levering van dynamische elementen die zijn niet bedoeld voor toobe in de cache opgeslagen of heel vaak worden bijgewerkt omdat Hallo CDN moet pull-een nieuwe versie van Hallo asset van de bronserver Hallo heel vaak.</span><span class="sxs-lookup"><span data-stu-id="4be9a-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="4be9a-193">Voor dit scenario kunt u inschakelen [dynamische Site-versnelling](cdn-dynamic-site-acceleration.md) optimalisatie (DSA) op uw CDN-eindpunt dat gebruikmaakt van verschillende technieken toospeed up levering van niet-caching geschikte dynamische activa.</span><span class="sxs-lookup"><span data-stu-id="4be9a-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="4be9a-194">Als u een site met een combinatie van statische en dynamische inhoud hebt, kunt u kiezen tooserve uw statische inhoud uit CDN met een statische optimalisatie type (zoals algemene webtoepassingen levering) en tooserve dynamische inhoud rechtstreeks vanaf de bronserver Hallo of via een CDN het eindpunt met DSA optimalisatie per geval ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4be9a-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="4be9a-195">einde toothat, u hebt al gezien hoe afzonderlijke inhoud tooaccess bestanden van Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="4be9a-196">Ik ziet u hoe tooserve een specifieke domeincontroller actie via een specifieke CDN-eindpunt in dienen uit controller acties via Azure CDN-inhoud.</span><span class="sxs-lookup"><span data-stu-id="4be9a-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="4be9a-197">Hallo alternatief is toodetermine die inhoud tooserve van Azure CDN op basis van geval in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4be9a-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="4be9a-198">einde toothat, u hebt al gezien hoe afzonderlijke inhoud tooaccess bestanden van Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="4be9a-199">Leest u hoe tooserve een specifieke domeincontroller actie via Hallo CDN-eindpunt in [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="4be9a-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="4be9a-200">Cacheopties voor statische bestanden in uw cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="4be9a-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="4be9a-201">U kunt opgeven hoe u statische inhoud toobe in de cache opgeslagen in de CDN-eindpunt hello wilt met Azure CDN-integratie in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="4be9a-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="4be9a-202">toodo deze, open *Web.config* van uw rol Web project (bijvoorbeeld WebRole1) en voeg een `<staticContent>` element te`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="4be9a-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="4be9a-203">Hallo XML onderstaande configureert Hallo cache tooexpire 3 dagen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="4be9a-204">Als u dit doet, ziet alle statische bestanden in uw cloudservice Hallo dezelfde regel in uw CDN-cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="4be9a-205">Voor gedetailleerde controle over de clientcache-instellingen, voegt u een *Web.config* bestand naar een map en uw instellingen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="4be9a-206">Bijvoorbeeld, Voeg een *Web.config* bestand toohello *\Content* map en vervang Hallo inhoud Hello XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="4be9a-207">Deze instelling zorgt ervoor dat alle statische bestanden van Hallo *\Content* map toobe 15 dagen in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="4be9a-208">Voor meer informatie over het tooconfigure hello `<clientCache>` element, Zie [clientcache &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="4be9a-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="4be9a-209">In [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller), ook leest u hoe u de cache-instellingen voor de controller actie resultaten in Hallo CDN cache kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="4be9a-210">Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="4be9a-211">Wanneer u een cloud service-Webrol met Azure CDN integreert, is relatief gemakkelijk tooserve inhoud van de domeincontroller acties via hello Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="4be9a-212">Anders dan voor uw cloud service rechtstreeks via Azure CDN (uitgelegd hierboven) [Maarten Balliauw](https://twitter.com/maartenballiauw) laat u zien hoe toodo deze met een leuk MemeGenerator controller in [korte wachttijden op Hallo web Hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="4be9a-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="4be9a-213">Ik zal gewoon reproduceer het hier.</span><span class="sxs-lookup"><span data-stu-id="4be9a-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="4be9a-214">Stel dat in uw cloudservice die u wilt toogenerate memes op basis van de installatiekopie van een jonge Chuck Norris (foto's door [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) zoals deze:</span><span class="sxs-lookup"><span data-stu-id="4be9a-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="4be9a-215">U hebt een eenvoudige `Index` hello meme actie waarmee klanten Hallo toospecify Hallo items in Hallo-installatiekopie wordt gegenereerd zodra ze boeken toohello actie.</span><span class="sxs-lookup"><span data-stu-id="4be9a-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="4be9a-216">Aangezien het Chuck Norris, u mag verwachten deze pagina toobecome sterk populaire globaal.</span><span class="sxs-lookup"><span data-stu-id="4be9a-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="4be9a-217">Dit is een goed voorbeeld van voor de semi dynamische inhoud met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="4be9a-218">Stappen Hallo hierboven toosetup deze controller actie:</span><span class="sxs-lookup"><span data-stu-id="4be9a-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="4be9a-219">In Hallo *\Controllers* map, maak een nieuw .cs bestand aangeroepen *MemeGeneratorController.cs* en vervang Hallo inhoud met Hallo de volgende code.</span><span class="sxs-lookup"><span data-stu-id="4be9a-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="4be9a-220">Ervoor tooreplace Hallo gemarkeerd deel worden met de naam van uw CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="4be9a-221">Met de rechtermuisknop in de standaard Hallo `Index()` actie en selecteer **weergave toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="4be9a-222">Accepteer de onderstaande Hallo-instellingen en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4be9a-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="4be9a-223">Open Hallo nieuwe *Views\MemeGenerator\Index.cshtml* en vervang Hallo inhoud door Hallo eenvoudig HTML-code voor het indienen van items hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="4be9a-224">Hallo-cloudservice opnieuw publiceren en te navigeren**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** in uw browser.</span><span class="sxs-lookup"><span data-stu-id="4be9a-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="4be9a-225">Wanneer u Hallo formulierwaarden te verzenden`/MemeGenerator/Index`, Hallo `Index_Post` actiemethode retourneert een koppeling toohello `Show` actiemethode met Hallo respectieve invoer-ID.</span><span class="sxs-lookup"><span data-stu-id="4be9a-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="4be9a-226">Wanneer u Hallo koppeling klikt, kunt u Hallo na code bereiken:</span><span class="sxs-lookup"><span data-stu-id="4be9a-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="4be9a-227">Als uw lokale foutopsporing is gekoppeld, krijgt u Hallo reguliere foutopsporing ervaring met een lokale omleiding.</span><span class="sxs-lookup"><span data-stu-id="4be9a-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="4be9a-228">Als deze wordt uitgevoerd in de cloudservice hello, wordt naar het omleiden:</span><span class="sxs-lookup"><span data-stu-id="4be9a-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="4be9a-229">Dit komt overeen met toohello oorsprong URL bij uw CDN-eindpunt te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="4be9a-230">Vervolgens kunt u Hallo `OutputCacheAttribute` -kenmerk op Hallo `Generate` methode-toospecify hoe Hallo actie resultaat moet worden in de cache, die Azure CDN wordt geacht.</span><span class="sxs-lookup"><span data-stu-id="4be9a-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="4be9a-231">Hallo-code hieronder opgeven voor de vervaldatum van een cache van 1 uur (3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="4be9a-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="4be9a-232">Evenzo kan u fungeren inhoud van elke domeincontroller actie in uw cloudservice via uw Azure CDN, met Hallo gewenst cache-instelling.</span><span class="sxs-lookup"><span data-stu-id="4be9a-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="4be9a-233">In de volgende sectie hello leest u hoe tooserve Hallo gebundeld en scripts en CSS via Azure CDN minified.</span><span class="sxs-lookup"><span data-stu-id="4be9a-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="4be9a-234">ASP.NET bundeling en minification integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4be9a-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="4be9a-235">Scripts en CSS stylesheets niet vaak worden gewijzigd en voornaamste kandidaten zijn voor hello Azure CDN-cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="4be9a-236">Levering Hallo gehele Webrol via uw Azure CDN is de eenvoudigste manier toointegrate Hallo bundeling en minification met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="4be9a-237">Echter, als u niet toodo dit wilt, leest u hoe toodo het behoud van Hallo gewenst ontwikkelaars ervaring voor ASP.NET bundeling en minification, zoals:</span><span class="sxs-lookup"><span data-stu-id="4be9a-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="4be9a-238">Goede foutopsporing modus ervaring</span><span class="sxs-lookup"><span data-stu-id="4be9a-238">Great debug mode experience</span></span>
* <span data-ttu-id="4be9a-239">Gestroomlijnde implementatie</span><span class="sxs-lookup"><span data-stu-id="4be9a-239">Streamlined deployment</span></span>
* <span data-ttu-id="4be9a-240">Onmiddellijke updates tooclients voor script/CSS versie-upgrades</span><span class="sxs-lookup"><span data-stu-id="4be9a-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="4be9a-241">Terugval mechanisme als uw CDN-eindpunt is mislukt</span><span class="sxs-lookup"><span data-stu-id="4be9a-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="4be9a-242">Codewijzigingen minimaliseren</span><span class="sxs-lookup"><span data-stu-id="4be9a-242">Minimize code modification</span></span>

<span data-ttu-id="4be9a-243">In Hallo **WebRole1** project dat u hebt gemaakt in [integreren van een Azure CDN-eindpunt met uw Azure-website en bedienen van statische inhoud in uw webpagina's van Azure CDN](#deploy)Open *App_Start\ BundleConfig.cs* en eens kijken Hallo `bundles.Add()` methodeaanroepen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="4be9a-244">Hallo eerst `bundles.Add()` instructie voegt u een script bundel op de virtuele map Hallo `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="4be9a-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="4be9a-245">Open vervolgens *Views\Shared\_Layout.cshtml* toosee hoe Hallo-scriptcode bundel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="4be9a-246">U moet kunnen toofind Hallo Razor coderegel te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="4be9a-247">Wanneer deze Razor code wordt uitgevoerd in Azure-Webrol hello, krijgt het een `<script>` tag voor Hallo bundel vergelijkbare toohello volgende script:</span><span class="sxs-lookup"><span data-stu-id="4be9a-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="4be9a-248">Echter, als deze wordt uitgevoerd in Visual Studio door te typen `F5`, geeft deze afzonderlijk elke scriptbestand in Hallo bundel weer (in Hallo geval bovenstaande slechts één scriptbestand is in de bundel Hallo):</span><span class="sxs-lookup"><span data-stu-id="4be9a-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="4be9a-249">Hiermee kunt u toodebug Hallo JavaScript-code in uw ontwikkelomgeving terwijl gelijktijdige clientverbindingen (bundeling) verminderen en het verbeteren van bestand prestaties (minification) in de productieomgeving downloaden.</span><span class="sxs-lookup"><span data-stu-id="4be9a-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="4be9a-250">Het is een uitstekende functie toopreserve met Azure CDN-integratie.</span><span class="sxs-lookup"><span data-stu-id="4be9a-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="4be9a-251">Bovendien omdat Hallo gerenderd bundel al een automatisch gegenereerde versietekenreeks bevat, gewenste tooreplicate die functionaliteit Hallo dus wanneer u uw jQuery-versie via NuGet, werken deze kan worden bijgewerkt op Hallo client zodra mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="4be9a-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="4be9a-252">Hallo stappen hieronder toointegration ASP.NET bundeling en minification met uw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="4be9a-253">Terug in de *App_Start\BundleConfig.cs*, Hallo wijzigen `bundles.Add()` methoden toouse een andere [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), die een CDN-adres.</span><span class="sxs-lookup"><span data-stu-id="4be9a-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="4be9a-254">toodo deze, Hallo vervangen `RegisterBundles` methodedefinitie Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="4be9a-255">Ervoor tooreplace worden `<yourCDNName>` met Hallo-naam van uw Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="4be9a-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="4be9a-256">In een gewone woorden die u instelt `bundles.UseCdn = true` en een zorgvuldig ontworpen CDN URL tooeach bundel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4be9a-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="4be9a-257">Bijvoorbeeld, Hallo eerste constructor Hallo code:</span><span class="sxs-lookup"><span data-stu-id="4be9a-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="4be9a-258">is hetzelfde als Hallo:</span><span class="sxs-lookup"><span data-stu-id="4be9a-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="4be9a-259">Deze constructor vertelt ASP.NET bundeling en minification toorender afzonderlijke scriptbestanden wanneer foutopsporing lokaal, maar gebruik Hallo opgegeven CDN adres tooaccess Hallo script in kwestie.</span><span class="sxs-lookup"><span data-stu-id="4be9a-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="4be9a-260">Let echter op twee belangrijke kenmerken met deze zorgvuldig ontworpen CDN-URL:</span><span class="sxs-lookup"><span data-stu-id="4be9a-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="4be9a-261">Hallo oorsprong voor dit CDN-URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, die eigenlijk Hallo virtuele map van Hallo script bundel in uw cloudservice is.</span><span class="sxs-lookup"><span data-stu-id="4be9a-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="4be9a-262">Aangezien u CDN constructor gebruikt, bevat Hallo CDN scriptcode voor Hallo-bundel niet langer versietekenreeks Hallo automatisch gegenereerd in Hallo URL weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="4be9a-263">Elke keer Hallo script bundel wordt gewijzigd tooforce een cache op uw Azure CDN gemist, moet u handmatig een unieke versietekenreeks genereren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="4be9a-264">AT Hallo dezelfde tijd, deze unieke versietekenreeks constante via Hallo levensduur van Hallo implementatie toomaximize cachetreffers op uw Azure CDN moet blijven nadat Hallo bundel is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4be9a-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="4be9a-265">Hallo queryreeks v = < W.X.Y.Z > worden van *Properties\AssemblyInfo.cs* in uw webproject rol.</span><span class="sxs-lookup"><span data-stu-id="4be9a-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="4be9a-266">U kunt een werkstroom voor de implementatie met Hallo assembly-versie wordt verhoogd telkens wanneer u tooAzure publiceren hebben.</span><span class="sxs-lookup"><span data-stu-id="4be9a-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="4be9a-267">Of u kunt alleen wijzigen *Properties\AssemblyInfo.cs* in uw project tooautomatically verhoging Hallo versietekenreeks telkens wanneer u bouwt, met behulp van Hallo jokerteken ' *'.</span><span class="sxs-lookup"><span data-stu-id="4be9a-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="4be9a-268">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4be9a-268">For example:</span></span>
     
        <span data-ttu-id="4be9a-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="4be9a-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="4be9a-270">Andere strategie-toostreamline genereren van een unieke tekenreeks voor Hallo levensduur van een implementatie wordt hier werken.</span><span class="sxs-lookup"><span data-stu-id="4be9a-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="4be9a-271">Opnieuw publiceren Hallo cloud-service en access Hallo startpagina.</span><span class="sxs-lookup"><span data-stu-id="4be9a-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="4be9a-272">Weergave hello HTML-code voor het Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="4be9a-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="4be9a-273">U moet kunnen toosee Hallo CDN URL weergegeven, met een unieke versietekenreeks telkens wanneer u wijzigingen tooyour cloudservice opnieuw publiceren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="4be9a-274">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4be9a-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="4be9a-275">Foutopsporing in Visual Studio Hallo cloudservice in Visual Studio door te typen `F5`.,</span><span class="sxs-lookup"><span data-stu-id="4be9a-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="4be9a-276">Weergave hello HTML-code voor het Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="4be9a-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="4be9a-277">U ziet nog steeds elke scriptbestand afzonderlijk weergegeven zodat u kunt een consistente foutopsporing optreden in Visual Studio hebben.</span><span class="sxs-lookup"><span data-stu-id="4be9a-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="4be9a-278">Terugval mechanisme voor CDN-URL 's</span><span class="sxs-lookup"><span data-stu-id="4be9a-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="4be9a-279">Als uw Azure CDN-eindpunt voor een of andere reden mislukt, wilt u uw webpagina toobe slimme voldoende tooaccess uw webserver oorsprong als terugvaloptie voor het laden van JavaScript of Bootstrap Hallo.</span><span class="sxs-lookup"><span data-stu-id="4be9a-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="4be9a-280">Het is ernstig genoeg toolose installatiekopieën op uw website vanwege tooCDN niet beschikbaar zijn, maar veel ernstiger toolose cruciaal pagina functionaliteit van uw scripts en stylesheets.</span><span class="sxs-lookup"><span data-stu-id="4be9a-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="4be9a-281">Hallo [bundel](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) klasse bevat een eigenschap genaamd [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) waarmee u tooconfigure Hallo terugval mechanisme voor CDN-fout.</span><span class="sxs-lookup"><span data-stu-id="4be9a-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="4be9a-282">toouse deze eigenschap, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="4be9a-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="4be9a-283">Open in uw webrolproject *App_Start\BundleConfig.cs*, waarin u een CDN-URL toegevoegd in elk [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), en zorg Hallo volgende gemarkeerd tooadd terugval mechanisme toohello wordt gewijzigd standaard-pakketten:</span><span class="sxs-lookup"><span data-stu-id="4be9a-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="4be9a-284">Wanneer `CdnFallbackExpression` is niet null script is opgenomen in Hallo HTML tootest of Hallo bundel is geladen en als dat niet Hallo bundel rechtstreeks vanuit Hallo oorsprong webserver openen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="4be9a-285">Deze eigenschap moet toobe set tooa JavaScript-expressie die wordt gecontroleerd of de respectieve CDN bundel Hallo correct wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="4be9a-286">Hallo expressie nodig tootest elke bundel verschilt volgens toohello inhoud.</span><span class="sxs-lookup"><span data-stu-id="4be9a-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="4be9a-287">Voor Hallo standaard bundels bovenstaande:</span><span class="sxs-lookup"><span data-stu-id="4be9a-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="4be9a-288">`window.jquery`is gedefinieerd in jquery-{version} .js</span><span class="sxs-lookup"><span data-stu-id="4be9a-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="4be9a-289">`$.validator`is gedefinieerd in jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="4be9a-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="4be9a-290">`window.Modernizr`is gedefinieerd in modernizer-{version} .js</span><span class="sxs-lookup"><span data-stu-id="4be9a-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="4be9a-291">`$.fn.modal`is gedefinieerd in bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="4be9a-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="4be9a-292">U mogelijk opgevallen dat ik CdnFallbackExpression niet is ingesteld voor Hallo `~/Cointent/css` bundel.</span><span class="sxs-lookup"><span data-stu-id="4be9a-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="4be9a-293">Dit is omdat er momenteel een [fout in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) die injects een `<script>` tag voor terugval CSS in plaats van Hallo verwacht Hallo `<link>` label.</span><span class="sxs-lookup"><span data-stu-id="4be9a-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="4be9a-294">Er is echter een goede [stijl bundel terugval](https://github.com/EmberConsultingGroup/StyleBundleFallback) die worden aangeboden door [Ember advies groep](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="4be9a-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="4be9a-295">toouse hello oplossing voor CSS en maak een nieuw .cs-bestand in uw webrolproject *App_Start* map met de naam *StyleBundleExtensions.cs*, en vervang de inhoud ervan Hello [code uit GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="4be9a-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="4be9a-296">In *App_Start\StyleFundleExtensions.cs*, Hallo naamruimte tooyour Webrol van naam (bijvoorbeeld **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="4be9a-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="4be9a-297">Ga terug te`App_Start\BundleConfig.cs` en Hallo laatste wijzigen `bundles.Add` instructie Hello gemarkeerde code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="4be9a-298">Deze nieuwe uitbreidingsmethode Hallo gebruikt dezelfde idee tooinject script in Hallo HTML toocheck Hallo DOM voor Hallo een overeenkomende klassenaam, regelnaam en regel waarde die is gedefinieerd in Hallo CSS-bundel en valt back toohello oorsprong webserver als deze uitvalt toofind Hallo overeen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="4be9a-299">Hallo cloud-service opnieuw en toegang Hallo-startpagina publiceren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="4be9a-300">Weergave hello HTML-code voor het Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="4be9a-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="4be9a-301">U moet de geïnjecteerde scripts vergelijkbare toohello volgende vinden:</span><span class="sxs-lookup"><span data-stu-id="4be9a-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="4be9a-302">Ingevoegd script voor Hallo CSS-bundel bevat nog steeds onjuiste restant Hallo van Hallo `CdnFallbackExpression` eigenschap in Hallo regel:</span><span class="sxs-lookup"><span data-stu-id="4be9a-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="4be9a-303">Maar omdat het eerste deel van de Hallo Hallo || expressie wordt altijd waar retourneren, (op Hallo regel boven die), Hallo document.write() functie wordt nooit uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4be9a-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="4be9a-304">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="4be9a-304">More Information</span></span>
* [<span data-ttu-id="4be9a-305">Overzicht van hello Azure Content Delivery Network (CDN)</span><span class="sxs-lookup"><span data-stu-id="4be9a-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="4be9a-306">Azure CDN gebruiken</span><span class="sxs-lookup"><span data-stu-id="4be9a-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="4be9a-307">ASP.NET bundeling en Minification</span><span class="sxs-lookup"><span data-stu-id="4be9a-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
