---
title: een Azure line-of-business-app met AD FS-authenticatie aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een line-of-business-app in Azure App Service die met verifieert lokale STS. Deze zelfstudie is bedoeld voor AD FS zoals Hallo lokale STS.
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="b197f-104">Een Azure line-of-business-app maken met AD FS-verificatie</span><span class="sxs-lookup"><span data-stu-id="b197f-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="b197f-105">Dit artikel ziet u hoe toocreate een ASP.NET MVC line-of-business-toepassing in [Azure App Service](../app-service/app-service-value-prop-what-is.md) met behulp van een on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) als Hallo id-provider.</span><span class="sxs-lookup"><span data-stu-id="b197f-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="b197f-106">Dit scenario kunt werken wanneer u wilt dat toocreate line-of-business-toepassingen in Azure App Service, maar uw organisatie directory gegevens toobe opgeslagen op de locatie vereist.</span><span class="sxs-lookup"><span data-stu-id="b197f-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="b197f-107">Zie voor een overzicht van Hallo verschillende enterprise verificatie en autorisatie opties voor Azure App Service [verifiëren met de lokale Active Directory in uw app in Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="b197f-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="b197f-108">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="b197f-108">What you will build</span></span>
<span data-ttu-id="b197f-109">Met de volgende kenmerken Hallo bouwt u een eenvoudige ASP.NET-toepassing in Azure App Service Web Apps:</span><span class="sxs-lookup"><span data-stu-id="b197f-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="b197f-110">Verificatie van gebruikers op basis van AD FS</span><span class="sxs-lookup"><span data-stu-id="b197f-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="b197f-111">Maakt gebruik van `[Authorize]` tooauthorize gebruikers voor verschillende acties</span><span class="sxs-lookup"><span data-stu-id="b197f-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="b197f-112">Statische configuratie voor zowel foutopsporing in Visual Studio en publiceren van tooApp Service Web Apps (één keer te configureren, fouten opsporen en op elk gewenst moment publiceren)</span><span class="sxs-lookup"><span data-stu-id="b197f-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="b197f-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="b197f-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="b197f-114">U moet volgen toocomplete Hallo in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="b197f-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="b197f-115">Een on-premises AD FS-implementatie (Zie voor een end-to-end-overzicht van testlab Hallo in deze zelfstudie gebruikt [van het testlab: zelfstandige STS met AD FS in Azure virtuele machine (voor test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="b197f-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="b197f-116">Machtigingen toocreate relying party-vertrouwensrelaties in AD FS-beheer</span><span class="sxs-lookup"><span data-stu-id="b197f-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="b197f-117">Visual Studio 2013 Update 4 of hoger</span><span class="sxs-lookup"><span data-stu-id="b197f-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="b197f-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) of hoger</span><span class="sxs-lookup"><span data-stu-id="b197f-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="b197f-119">Voorbeeld van een toepassing gebruiken voor line-of-business-sjabloon</span><span class="sxs-lookup"><span data-stu-id="b197f-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="b197f-120">Voorbeeld van een toepassing in deze zelfstudie Hallo [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), door hello Azure Active Directory-team is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b197f-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="b197f-121">Aangezien AD FS WS-Federation ondersteunt, kunt u deze gebruiken als een sjabloon toocreate line-of-business-toepassingen met gemak.</span><span class="sxs-lookup"><span data-stu-id="b197f-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="b197f-122">Hallo volgende kenmerken heeft:</span><span class="sxs-lookup"><span data-stu-id="b197f-122">It has hello following features:</span></span>

* <span data-ttu-id="b197f-123">Maakt gebruik van [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate met een on-premises AD FS-implementatie</span><span class="sxs-lookup"><span data-stu-id="b197f-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="b197f-124">Functionaliteit voor aanmelden en afmelden</span><span class="sxs-lookup"><span data-stu-id="b197f-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="b197f-125">Maakt gebruik van [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (in plaats van Windows Identity Foundation), die is Hallo toekomstige van ASP.NET en veel eenvoudiger tooset voor verificatie en autorisatie dan WIF</span><span class="sxs-lookup"><span data-stu-id="b197f-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="b197f-126">Hallo-voorbeeldtoepassing instellen</span><span class="sxs-lookup"><span data-stu-id="b197f-126">Set up hello sample application</span></span>
1. <span data-ttu-id="b197f-127">Klonen of downloaden Hallo Voorbeeldoplossing op [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour lokale map.</span><span class="sxs-lookup"><span data-stu-id="b197f-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b197f-128">instructies op Hallo [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) laten zien hoe u tooset Hallo-toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b197f-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="b197f-129">Maar in deze zelfstudie maakt u instellen met AD FS, dus stappen Hallo hier in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="b197f-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="b197f-130">Open Hallo oplossing en open vervolgens Controllers\AccountController.cs in Hallo **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b197f-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="b197f-131">U ziet dat Hallo code gewoon een authentication uitdaging tooauthenticate Hallo-gebruiker met behulp van WS-Federation uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="b197f-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="b197f-132">Alle verificatie is geconfigureerd in App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="b197f-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="b197f-133">Open App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="b197f-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="b197f-134">In Hallo `ConfigureAuth` methode, opmerking Hallo regel:</span><span class="sxs-lookup"><span data-stu-id="b197f-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="b197f-135">In OWIN-wereld Hallo is is in dit fragment in feite Hallo bare dat minimum moet u tooconfigure WS-Federation-verificatie.</span><span class="sxs-lookup"><span data-stu-id="b197f-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="b197f-136">Het is veel eenvoudiger en meer elegante dan WIF, waarbij Web.config met XML wordt geïnjecteerd over Hallo plaats.</span><span class="sxs-lookup"><span data-stu-id="b197f-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="b197f-137">Hallo enige informatie die u nodig Hallo van de partij (RP is)-ID en het Hallo-URL van uw AD FS-service-metagegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="b197f-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="b197f-138">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b197f-138">Here's an example:</span></span>
   
   * <span data-ttu-id="b197f-139">RP-id:`https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="b197f-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="b197f-140">Adres van de metagegevens:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="b197f-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="b197f-141">Wijzig in App_Start\Startup.Auth.cs, Hallo statische tekenreeks definities te volgen:</span><span class="sxs-lookup"><span data-stu-id="b197f-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="b197f-142">Nu Hallo bijbehorende wijzigingen aanbrengen in het bestand Web.config. Open Web.config Hallo en Hallo volgende app-instellingen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="b197f-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="b197f-143">Vul in op basis van uw omgeving respectieve Hallo-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="b197f-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="b197f-144">Bouw Hallo toepassing toomake ervoor dat er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="b197f-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="b197f-145">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="b197f-145">That's it.</span></span> <span data-ttu-id="b197f-146">Hallo-voorbeeldtoepassing is nu gereed toowork met AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="b197f-147">U moet nog steeds tooconfigure een RP-vertrouwensrelatie met deze toepassing in AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="b197f-148">Hallo voorbeeld toepassing tooAzure App Service Web Apps implementeren</span><span class="sxs-lookup"><span data-stu-id="b197f-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="b197f-149">Hier kunt publiceren u Hallo toepassing tooa web-app in App Service Web Apps behoud Hallo foutopsporing omgeving.</span><span class="sxs-lookup"><span data-stu-id="b197f-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="b197f-150">Houd er rekening mee dat u toopublish Hallo toepassing gaat voordat er een RP-vertrouwensrelatie met AD FS, zodat verificatie nog steeds niet nog werkt.</span><span class="sxs-lookup"><span data-stu-id="b197f-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="b197f-151">Als u deze kunt nu u wel Hallo web app-URL die u later tooconfigure Hallo RP vertrouwensrelatie kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b197f-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="b197f-152">Met de rechtermuisknop op uw project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="b197f-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="b197f-153">Selecteer **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="b197f-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="b197f-154">Als u dit nog niet hebt aangemeld tooAzure, klikt u op **aanmelden** en Hallo Microsoft-account gebruiken voor uw Azure-abonnement toosign in.</span><span class="sxs-lookup"><span data-stu-id="b197f-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="b197f-155">Nadat u bent aangemeld, klikt u op **nieuw** toocreate een web-app.</span><span class="sxs-lookup"><span data-stu-id="b197f-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="b197f-156">Vul alle verplichte velden.</span><span class="sxs-lookup"><span data-stu-id="b197f-156">Fill in all required fields.</span></span> <span data-ttu-id="b197f-157">U gaat tooconnect tooon-premises gegevens later, zodat een database voor deze web-app niet maken.</span><span class="sxs-lookup"><span data-stu-id="b197f-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="b197f-158">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b197f-158">Click **Create**.</span></span> <span data-ttu-id="b197f-159">Zodra Hallo web-app is gemaakt, wordt Hallo webpublicatie dialoogvenster geopend.</span><span class="sxs-lookup"><span data-stu-id="b197f-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="b197f-160">In **doel-URL**, wijzigen **http** te**https**.</span><span class="sxs-lookup"><span data-stu-id="b197f-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="b197f-161">Kopieer Hallo volledige URL tooa teksteditor voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="b197f-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="b197f-162">Klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="b197f-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="b197f-163">Open in Visual Studio **Web.Release.config** in uw project.</span><span class="sxs-lookup"><span data-stu-id="b197f-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="b197f-164">Invoegen na XML in Hallo Hallo `<configuration>` labelen en Hallo sleutelwaarde vervangen door uw publish web-app-URL.</span><span class="sxs-lookup"><span data-stu-id="b197f-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="b197f-165">Wanneer u bent klaar, hebt u twee RP id's die worden geconfigureerd in uw project, één voor uw omgeving voor foutopsporing in Visual Studio en één voor Hallo web-app in Azure hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="b197f-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="b197f-166">Stelt u een vertrouwensrelatie RP voor elk van de twee omgevingen Hallo in AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="b197f-167">Tijdens de foutopsporing, Hallo app-instellingen in Web.config gebruikte toomake zijn uw **Debug** configuratie werken met AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="b197f-168">Wanneer deze wordt gepubliceerd (standaard Hallo **Release** configuratie wordt gepubliceerd), een getransformeerde Web.config waarin Hallo appwijzigingen van de instelling in Web.Release.config wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="b197f-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="b197f-169">Als u wilt dat tooattach Hallo gepubliceerde web-app in Azure toohello foutopsporingsprogramma (dat wil zeggen moet u de symbolen foutopsporing van uw code in Hallo gepubliceerde web-app uploaden), kunt u een kloon van Hallo fouten opsporen in de configuratie voor foutopsporing in Azure, maar met een eigen aangepaste Web.config Transformeren) bijvoorbeeld Web.AzureDebug.config) die gebruikmaakt van app-instellingen van Web.Release.config Hallo. Hiermee kunt u een statische configuratie toomaintain in verschillende omgevingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b197f-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="b197f-170">Vertrouwensrelaties met relying party's in AD FS-beheer configureren</span><span class="sxs-lookup"><span data-stu-id="b197f-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="b197f-171">Nu moet u een vertrouwensrelatie RP in AD FS-beheer tooconfigure voordat u kunt uw voorbeeldtoepassing gebruiken en daadwerkelijk met AD FS verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b197f-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="b197f-172">U moet tooset van twee afzonderlijke RP-vertrouwensrelaties, één voor uw omgeving voor foutopsporing en één voor de gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="b197f-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="b197f-173">Zorg ervoor dat u de volgende stappen uit voor zowel uw omgevingen Hallo herhaalt.</span><span class="sxs-lookup"><span data-stu-id="b197f-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="b197f-174">Aanmelden met referenties die tooAD van de rights management FS hebben op uw AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="b197f-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="b197f-175">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="b197f-175">Open AD FS Management.</span></span> <span data-ttu-id="b197f-176">Met de rechtermuisknop op **AD FS\Trusted Relationships\Relying Party-vertrouwensrelaties** en selecteer **Relying Party Trust toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b197f-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="b197f-177">In Hallo **gegevensbron selecteren** pagina **gegevens over Hallo relying party handmatig invoeren**.</span><span class="sxs-lookup"><span data-stu-id="b197f-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="b197f-178">In Hallo **weergavenaam opgeven** pagina, typ een weergavenaam voor de toepassing hello en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="b197f-179">In Hallo **Protocol kiezen** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="b197f-180">In Hallo **certificaat configureren** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b197f-181">Omdat u moet worden gebruikt voor HTTPS al, is versleuteld tokens zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="b197f-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="b197f-182">Als u echt tooencrypt tokens van AD FS op deze pagina wilt, moet u ook logica tokenontsleuteling toevoegen in uw code.</span><span class="sxs-lookup"><span data-stu-id="b197f-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="b197f-183">Zie voor meer informatie [handmatig OWIN WS-Federation-middleware configureren en het accepteren van tokens versleuteld](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="b197f-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="b197f-184">Voordat u naar de volgende stap hello verplaatst, moet u een stukje informatie van uw Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="b197f-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="b197f-185">In de Projecteigenschappen hello, houd er rekening mee Hallo **SSL URL** van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b197f-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="b197f-186">Terug in AD FS-beheer in Hallo **URL configureren** pagina Hallo **toevoegen Wizard Relying Party Trust**, selecteer **ondersteuning voor Hallo WS-Federation Passive protocol inschakelen** en Typ in Hallo SSL-URL van uw Visual Studio-project dat u hebt genoteerd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="b197f-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="b197f-187">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="b197f-188">URL bevat waar toosend Hallo client na verificatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="b197f-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="b197f-189">Hallo foutopsporing omgeving moet <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="b197f-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="b197f-190">Voor Hallo gepubliceerde web-app moet het Hallo web-app-URL.</span><span class="sxs-lookup"><span data-stu-id="b197f-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="b197f-191">In Hallo **id's configureren** pagina, controleert u of de SSL-URL van uw project al is vermeld en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="b197f-192">Klik op **volgende** alle Hallo manier toohello einde van de standaardselecties Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="b197f-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b197f-193">In App_Start\Startup.Auth.cs van Visual Studio-project deze id wordt vergeleken met de waarde van Hallo <code>WsFederationAuthenticationOptions.Wtrealm</code> tijdens federatieve verificatie.</span><span class="sxs-lookup"><span data-stu-id="b197f-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="b197f-194">Standaard wordt van de toepassing hello-URL van de vorige stap Hallo toegevoegd als een RP-id.</span><span class="sxs-lookup"><span data-stu-id="b197f-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="b197f-195">U bent nu klaar Hallo RP-toepassing voor uw project in AD FS configureren.</span><span class="sxs-lookup"><span data-stu-id="b197f-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="b197f-196">Vervolgens configureert u deze toepassing toosend Hallo claims die nodig is voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b197f-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="b197f-197">Hallo **Claimregels bewerken** dialoogvenster wordt standaard voor u geopend aan einde van de wizard Hallo Hallo zodat u meteen kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="b197f-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="b197f-198">We gaan configureren ten minste Hallo volgende claims (met schema's tussen haakjes):</span><span class="sxs-lookup"><span data-stu-id="b197f-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="b197f-199">Naam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - gebruikt door ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="b197f-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="b197f-200">Gebruiker (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - UPN gebruikt toouniquely Identificeer gebruikers in het Hallo-organisatie.</span><span class="sxs-lookup"><span data-stu-id="b197f-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="b197f-201">Groepslidmaatschappen als (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - rollen kan worden gebruikt met `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize domeincontrollers/acties.</span><span class="sxs-lookup"><span data-stu-id="b197f-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="b197f-202">In werkelijkheid is kan deze methode niet worden Hallo meeste zodat voor rolautorisatie.</span><span class="sxs-lookup"><span data-stu-id="b197f-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="b197f-203">Als uw AD-gebruikers toohundreds van beveiligingsgroepen behoren, worden ze honderden rolclaims in Hallo SAML-token.</span><span class="sxs-lookup"><span data-stu-id="b197f-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="b197f-204">Een alternatieve methode is toosend één rol claim voorwaardelijk afhankelijk van Hallo gebruiker lid is van een bepaalde groep.</span><span class="sxs-lookup"><span data-stu-id="b197f-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="b197f-205">Maar je we Houd het eenvoudig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b197f-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="b197f-206">Gebruikersnaam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - kunnen worden gebruikt voor validatie antivirusprogramma kunnen worden vervalst.</span><span class="sxs-lookup"><span data-stu-id="b197f-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="b197f-207">Zie voor meer informatie over hoe de toomake is werken met ter voorkoming validatie, Hallo **line-of-business-functionaliteit toevoegen** sectie van [een Azure line-of-business-app maken met Azure Active Directory-verificatie ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="b197f-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b197f-208">Hallo claim typt u tooconfigure nodig hebt voor uw toepassing wordt bepaald door de behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b197f-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="b197f-209">Hallo-lijst met claims die worden ondersteund door Azure Active Directory-toepassingen (dat wil zeggen RP-vertrouwensrelaties), bijvoorbeeld zien [ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="b197f-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="b197f-210">Klik in het dialoogvenster Claimregels bewerken Hallo **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b197f-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="b197f-211">Hallo-naam, UPN en rol claims configureren, zoals weergegeven in de schermafbeelding Hallo en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b197f-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="b197f-212">Maak vervolgens een tijdelijke naam ID claim in met behulp van Hallo stappen uitgelegd [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="b197f-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="b197f-213">Klik op **regel toevoegen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b197f-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="b197f-214">Selecteer **Claims verzenden met een aangepaste regel** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="b197f-215">Plakken Hallo volgende regel taal in Hallo **aangepaste regel** vak, naam Hallo regel **Per sessie-id** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b197f-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="b197f-216">Uw aangepaste regel moet eruitzien als in deze schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="b197f-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="b197f-217">Klik op **regel toevoegen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b197f-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="b197f-218">Selecteer **een binnenkomende Claim transformeren** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b197f-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="b197f-219">Hallo regel configureren, zoals weergegeven in Hallo schermafbeelding (met claimtype Hallo u hebt gemaakt in een aangepaste regel Hallo) en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b197f-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="b197f-220">Zie voor gedetailleerde informatie over Hallo stappen voor het Hallo tijdelijke naam-ID claim [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="b197f-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="b197f-221">Klik op **toepassen** in Hallo **Claimregels bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b197f-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="b197f-222">Deze ziet er nu als Hallo schermafbeelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="b197f-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="b197f-223">Zorg ervoor dat u deze stappen herhalen voor uw omgeving voor foutopsporing en de gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="b197f-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="b197f-224">Federatieve verificatie voor uw toepassing testen</span><span class="sxs-lookup"><span data-stu-id="b197f-224">Test federated authentication for your application</span></span>
<span data-ttu-id="b197f-225">U bent gereed tootest verificatielogica van uw toepassing op basis van AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="b197f-226">Ik heb een testgebruiker die deel uitmaakt van tooa testgroep in Active Directory (AD) in de AD FS-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b197f-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="b197f-227">tootest verificatie in Hallo foutopsporingsprogramma, hoeft u toodo nu is type `F5`.</span><span class="sxs-lookup"><span data-stu-id="b197f-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="b197f-228">Als u tootest verificatie in Hallo gepubliceerde web-app wilt, navigeer toohello URL.</span><span class="sxs-lookup"><span data-stu-id="b197f-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="b197f-229">Nadat het Hallo-webtoepassing is geladen, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="b197f-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="b197f-230">Nu moet u ofwel een dialoogvenster of Hallo aanmelding aanmeldingspagina afgehandeld door AD FS is afhankelijk van de verificatiemethode Hallo gekozen door AD FS.</span><span class="sxs-lookup"><span data-stu-id="b197f-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="b197f-231">Hier volgt ik in Internet Explorer 11 krijgen.</span><span class="sxs-lookup"><span data-stu-id="b197f-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="b197f-232">Zodra u aanmelden als gebruiker in Hallo AD-domein van Hallo AD FS-implementatie, u ziet nu Hallo startpagina opnieuw met **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="b197f-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="b197f-233">Hallo klikken in.</span><span class="sxs-lookup"><span data-stu-id="b197f-233">in hello corner.</span></span> <span data-ttu-id="b197f-234">Hier volgt krijg ik.</span><span class="sxs-lookup"><span data-stu-id="b197f-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="b197f-235">U hebt tot nu toe is voltooid in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="b197f-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="b197f-236">Uw toepassing heeft de AD FS is bereikt en een overeenkomende RP-id is gevonden in Hallo AD FS-database</span><span class="sxs-lookup"><span data-stu-id="b197f-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="b197f-237">AD FS is geverifieerd een AD-gebruiker en u een back-startpagina van de toepassing toohello-omleiding</span><span class="sxs-lookup"><span data-stu-id="b197f-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="b197f-238">AD FS als de naam van de verzonden hello claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour toepassing, zoals aangegeven door Hallo feit die gebruiker Hallo naam wordt weergegeven in Hallo hoek.</span><span class="sxs-lookup"><span data-stu-id="b197f-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="b197f-239">Als de naamclaim Hallo ontbreekt, u zou hebben gezien **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="b197f-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="b197f-240">Als u Views\Shared bekijkt\_LoginPartial.cshtml, vindt u die gebruikmaakt van `User.Identity.Name` toodisplay Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="b197f-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="b197f-241">Zoals eerder vermeld als Hallo naam claim Hallo geverifieerde gebruiker is beschikbaar in Hallo SAML-token, hydrates ASP.NET deze eigenschap aan.</span><span class="sxs-lookup"><span data-stu-id="b197f-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="b197f-242">alle Hallo toosee claims worden verzonden door AD FS, een onderbrekingspunt in Controllers\HomeController.cs, plaatsen in de Hallo Index actiemethode.</span><span class="sxs-lookup"><span data-stu-id="b197f-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="b197f-243">Nadat het Hallo-gebruiker is geverifieerd, inspecteren Hallo `System.Security.Claims.Current.Claims` verzameling.</span><span class="sxs-lookup"><span data-stu-id="b197f-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="b197f-244">Autoriseren van gebruikers voor specifieke domeincontrollers of acties</span><span class="sxs-lookup"><span data-stu-id="b197f-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="b197f-245">Aangezien u groepslidmaatschappen als rolclaims in uw configuratie van de vertrouwensrelatie RP hebt opgenomen, kunt u nu gebruiken ze rechtstreeks in Hallo `[Authorize(Roles="...")]` decoration voor domeincontrollers en acties.</span><span class="sxs-lookup"><span data-stu-id="b197f-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="b197f-246">In een line-of-business-toepassing met Hallo maken, lezen, bijwerken, verwijderen (CRUD) patroon, kunt u specifieke rollen tooaccess elke actie autoriseren.</span><span class="sxs-lookup"><span data-stu-id="b197f-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="b197f-247">Op dit moment wordt u alleen deze functie op Hallo bestaande Home domeincontroller uitproberen.</span><span class="sxs-lookup"><span data-stu-id="b197f-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="b197f-248">Open Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="b197f-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="b197f-249">Hallo opmaken `About` en `Contact` actie methoden vergelijkbaar toohello de volgende code, met behulp van de geverifieerde gebruiker heeft beveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="b197f-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="b197f-250">Nadat ik toegevoegd **testgebruiker** te**testgroep** in mijn AD FS-testomgeving ik testgroep tootest autorisatie gebruik op `About`.</span><span class="sxs-lookup"><span data-stu-id="b197f-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="b197f-251">Voor `Contact`, test ik Hallo negatieve geval van **Domeinadministrators**, toowhich **gebruiker testen** behoort niet toe.</span><span class="sxs-lookup"><span data-stu-id="b197f-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="b197f-252">Hallo-foutopsporingsprogramma start door te typen `F5` en meld u aan en klik vervolgens op **over**.</span><span class="sxs-lookup"><span data-stu-id="b197f-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="b197f-253">U moet nu worden bekijkt hello `~/About/Index` pagina geslaagd, als de geverifieerde gebruiker is gemachtigd voor deze actie.</span><span class="sxs-lookup"><span data-stu-id="b197f-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="b197f-254">Klik nu op **Contact**, die in mijn geval dienen niet toe te staan **testgebruiker** voor Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="b197f-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="b197f-255">Hallo browser is echter omgeleide tooAD FS, die uiteindelijk ziet u dit bericht:</span><span class="sxs-lookup"><span data-stu-id="b197f-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="b197f-256">Als u deze fout in Logboeken op Hallo AD FS-server onderzoeken, ziet u dit bericht van uitzondering:</span><span class="sxs-lookup"><span data-stu-id="b197f-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="b197f-257">Hallo reden voor deze fout is dat standaard MVC retourneert een 401 niet geautoriseerd wanneer rollen van een gebruiker bent niet gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="b197f-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="b197f-258">Dit activeert een herauthenticatie aanvraag tooyour id-provider (AD FS).</span><span class="sxs-lookup"><span data-stu-id="b197f-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="b197f-259">Aangezien het Hallo-gebruiker is al geverifieerd, AD FS toohello retourneert dezelfde pagina die u vervolgens een andere 401 verstrekt, een lus omleiding maken.</span><span class="sxs-lookup"><span data-stu-id="b197f-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="b197f-260">Overschrijft u de AuthorizeAttribute `HandleUnauthorizedRequest` methode met een eenvoudige logische tooshow iets wat zinvol in plaats van de bewerking wordt voortgezet Hallo omleidings-lus.</span><span class="sxs-lookup"><span data-stu-id="b197f-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="b197f-261">Maak een bestand in Hallo project met de naam AuthorizeAttribute.cs en plakken Hallo code in het volgende.</span><span class="sxs-lookup"><span data-stu-id="b197f-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="b197f-262">Hallo code verzendt een HTTP 403 (verboden) in plaats van 401 HTTP-(niet-geautoriseerd) in geverifieerde maar niet-geautoriseerde gevallen overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b197f-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="b197f-263">Voer Hallo foutopsporingsprogramma opnieuw met `F5`.</span><span class="sxs-lookup"><span data-stu-id="b197f-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="b197f-264">Te klikken op **Contact** nu een meer informatieve (die mogelijk zwartwitprinter) foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b197f-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="b197f-265">Hallo toepassing tooAzure App Service Web Apps opnieuw publiceren en te testen Hallo gedrag van Hallo live-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b197f-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="b197f-266">Verbinding maken met tooon lokale gegevens</span><span class="sxs-lookup"><span data-stu-id="b197f-266">Connect tooon-premises data</span></span>
<span data-ttu-id="b197f-267">Een reden is dat u tooimplement uw line-of-business-toepassing met AD FS in plaats van Azure Active Directory wilt problemen met de compatibiliteit met het up-to-date houden organisatie gegevens uit de lokale.</span><span class="sxs-lookup"><span data-stu-id="b197f-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="b197f-268">Dit kan ook betekenen dat uw web-app in Azure toegang lokale databases, tot moet omdat het is niet toegestaan toouse [SQL-Database](/services/sql-database/) als gegevenslaag Hallo voor uw web-apps.</span><span class="sxs-lookup"><span data-stu-id="b197f-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="b197f-269">Azure App Service Web Apps biedt ondersteuning voor toegang tot lokale databases met twee benaderingen: [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [virtuele netwerken](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b197f-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="b197f-270">Zie voor meer informatie [VNET met behulp van integratie en hybride verbindingen met Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="b197f-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="b197f-271">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="b197f-271">Further resources</span></span>
* [<span data-ttu-id="b197f-272">Verificatie met de on-premises Active Directory in uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="b197f-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="b197f-273">Een Azure line-of-business-app maken met Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="b197f-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="b197f-274">Gebruik Hallo On-Premises organisatie verificatie optie (ADFS) met ASP.NET in Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b197f-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="b197f-275">Een tooKatana VS2013 Web Project van WIF migreren</span><span class="sxs-lookup"><span data-stu-id="b197f-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="b197f-276">Overzicht van Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="b197f-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="b197f-277">1.1 van WS-Federation-specificatie</span><span class="sxs-lookup"><span data-stu-id="b197f-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

