---
title: Een Azure line-of-business-app maken met AD FS-verificatie | Microsoft Docs
description: Informatie over het maken van een line-of-business-app in Azure App Service die wordt geverifieerd met lokale STS. Deze zelfstudie is bedoeld voor AD FS als de lokale STS.
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="56fc7-104">Een Azure line-of-business-app maken met AD FS-verificatie</span><span class="sxs-lookup"><span data-stu-id="56fc7-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="56fc7-105">Dit artikel ziet u het maken van een ASP.NET MVC-line-of-business-toepassing in [Azure App Service](../app-service/app-service-value-prop-what-is.md) met behulp van een on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) als de id-provider.</span><span class="sxs-lookup"><span data-stu-id="56fc7-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="56fc7-106">Dit scenario kunt werken wanneer u wilt maken van line-of-business-toepassingen in Azure App Service, maar uw organisatie vereist dat directorygegevens op de locatie worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="56fc7-107">Zie voor een overzicht van de andere enterprise-verificatie en autorisatie opties voor Azure App Service [verifiëren met de lokale Active Directory in uw app in Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="56fc7-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="56fc7-108">Wat u bouwt</span><span class="sxs-lookup"><span data-stu-id="56fc7-108">What you will build</span></span>
<span data-ttu-id="56fc7-109">Maakt u een eenvoudige ASP.NET-toepassing in Azure App Service Web Apps met de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="56fc7-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="56fc7-110">Verificatie van gebruikers op basis van AD FS</span><span class="sxs-lookup"><span data-stu-id="56fc7-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="56fc7-111">Maakt gebruik van `[Authorize]` voor het autoriseren van gebruikers voor verschillende acties</span><span class="sxs-lookup"><span data-stu-id="56fc7-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="56fc7-112">Statische configuratie voor zowel foutopsporing in Visual Studio en publiceren naar App Service Web Apps (één keer te configureren, fouten opsporen en op elk gewenst moment publiceren)</span><span class="sxs-lookup"><span data-stu-id="56fc7-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="56fc7-113">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="56fc7-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="56fc7-114">U moet het volgende om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="56fc7-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="56fc7-115">Een on-premises AD FS-implementatie (Zie voor een end-to-end-overzicht van het testlab in deze zelfstudie gebruikt [van het testlab: zelfstandige STS met AD FS in Azure virtuele machine (voor test)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="56fc7-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="56fc7-116">Machtigingen voor het maken van de relying partij vertrouwensrelaties in AD FS-beheer</span><span class="sxs-lookup"><span data-stu-id="56fc7-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="56fc7-117">Visual Studio 2013 Update 4 of hoger</span><span class="sxs-lookup"><span data-stu-id="56fc7-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="56fc7-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) of hoger</span><span class="sxs-lookup"><span data-stu-id="56fc7-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="56fc7-119">Voorbeeld van een toepassing gebruiken voor line-of-business-sjabloon</span><span class="sxs-lookup"><span data-stu-id="56fc7-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="56fc7-120">De voorbeeldtoepassing in deze zelfstudie [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is gemaakt door het team van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56fc7-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="56fc7-121">Aangezien AD FS WS-Federation ondersteunt, kunt u deze als sjabloon gebruiken line-of-business-toepassingen maken met gemak.</span><span class="sxs-lookup"><span data-stu-id="56fc7-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="56fc7-122">Het bevat de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="56fc7-122">It has the following features:</span></span>

* <span data-ttu-id="56fc7-123">Maakt gebruik van [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) voor verificatie met een on-premises AD FS-implementatie</span><span class="sxs-lookup"><span data-stu-id="56fc7-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="56fc7-124">Functionaliteit voor aanmelden en afmelden</span><span class="sxs-lookup"><span data-stu-id="56fc7-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="56fc7-125">Maakt gebruik van [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (in plaats van Windows Identity Foundation), dat wil zeggen de toekomstige van ASP.NET en veel eenvoudiger om in te stellen voor verificatie en autorisatie dan WIF</span><span class="sxs-lookup"><span data-stu-id="56fc7-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="56fc7-126">Instellen van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="56fc7-126">Set up the sample application</span></span>
1. <span data-ttu-id="56fc7-127">Klonen of downloaden van de Voorbeeldoplossing in [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) naar uw lokale map.</span><span class="sxs-lookup"><span data-stu-id="56fc7-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56fc7-128">De instructies op de [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) beschreven hoe u met het instellen van de toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56fc7-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="56fc7-129">Maar in deze zelfstudie maakt u instellen met AD FS, volg daarom de volgende stappen uit in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="56fc7-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="56fc7-130">Open de oplossing en open vervolgens Controllers\AccountController.cs in de **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="56fc7-131">U ziet dat de code gewoon een verificatiecontrole voor het verifiëren met behulp van WS-Federation uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="56fc7-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="56fc7-132">Alle verificatie is geconfigureerd in App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="56fc7-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="56fc7-133">Open App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="56fc7-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="56fc7-134">In de `ConfigureAuth` methode, Let op de regel:</span><span class="sxs-lookup"><span data-stu-id="56fc7-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="56fc7-135">In de wereld OWIN is in dit fragment in feite minimaal moet u WS-Federation-verificatie configureren.</span><span class="sxs-lookup"><span data-stu-id="56fc7-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="56fc7-136">Het is veel eenvoudiger en meer elegante dan WIF, waarbij Web.config met XML is ingevoegd in de plaats.</span><span class="sxs-lookup"><span data-stu-id="56fc7-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="56fc7-137">De enige informatie die u nodig is de relying party van (RP)-ID en de URL van het metagegevensbestand van uw AD FS-service.</span><span class="sxs-lookup"><span data-stu-id="56fc7-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="56fc7-138">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="56fc7-138">Here's an example:</span></span>
   
   * <span data-ttu-id="56fc7-139">RP-id:`https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="56fc7-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="56fc7-140">Adres van de metagegevens:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="56fc7-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="56fc7-141">Op App_Start\Startup.Auth.cs, wijzigt u de volgende definities van de vaste tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="56fc7-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="56fc7-142">Nu de bijbehorende wijzigingen aanbrengen in het bestand Web.config.</span><span class="sxs-lookup"><span data-stu-id="56fc7-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="56fc7-143">Open het bestand Web.config en de volgende appinstellingen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="56fc7-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="56fc7-144">Vul in de sleutelwaarden op basis van de respectieve omgeving.</span><span class="sxs-lookup"><span data-stu-id="56fc7-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="56fc7-145">Maken van de toepassing om te controleren of dat er zijn geen fouten.</span><span class="sxs-lookup"><span data-stu-id="56fc7-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="56fc7-146">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="56fc7-146">That's it.</span></span> <span data-ttu-id="56fc7-147">De voorbeeldtoepassing is nu gereed voor gebruik met AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="56fc7-148">U moet nog steeds een vertrouwensrelatie RP met deze toepassing in AD FS configureren.</span><span class="sxs-lookup"><span data-stu-id="56fc7-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="56fc7-149">De voorbeeldtoepassing op Azure App Service Web Apps implementeren</span><span class="sxs-lookup"><span data-stu-id="56fc7-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="56fc7-150">Hier kunt publiceren u de toepassing naar een web-app in App Service Web Apps behoud de foutopsporing-omgeving.</span><span class="sxs-lookup"><span data-stu-id="56fc7-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="56fc7-151">Houd er rekening mee dat u gaat de toepassing publiceren voordat er een RP-vertrouwensrelatie met AD FS, zodat verificatie nog steeds niet nog werkt.</span><span class="sxs-lookup"><span data-stu-id="56fc7-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="56fc7-152">Als u deze kunt nu u wel de app-URL die u gebruiken kunt voor het configureren van de vertrouwensrelatie RP later.</span><span class="sxs-lookup"><span data-stu-id="56fc7-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="56fc7-153">Met de rechtermuisknop op uw project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="56fc7-154">Selecteer **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="56fc7-155">Als u dit nog niet hebt aangemeld bij Azure, klikt u op **aanmelden** en gebruiken van het Microsoft-account voor uw Azure-abonnement aan te melden.</span><span class="sxs-lookup"><span data-stu-id="56fc7-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="56fc7-156">Nadat u bent aangemeld, klikt u op **nieuw** voor het maken van een web-app.</span><span class="sxs-lookup"><span data-stu-id="56fc7-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="56fc7-157">Vul alle verplichte velden.</span><span class="sxs-lookup"><span data-stu-id="56fc7-157">Fill in all required fields.</span></span> <span data-ttu-id="56fc7-158">U wilt verbinding maken met on-premises gegevens later, zodat een database voor deze web-app niet maken.</span><span class="sxs-lookup"><span data-stu-id="56fc7-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="56fc7-159">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-159">Click **Create**.</span></span> <span data-ttu-id="56fc7-160">Zodra de web-app is gemaakt, wordt het dialoogvenster Publish Web geopend.</span><span class="sxs-lookup"><span data-stu-id="56fc7-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="56fc7-161">In **doel-URL**, wijzigen **http** naar **https**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="56fc7-162">Kopieer de volledige URL naar een teksteditor voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="56fc7-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="56fc7-163">Klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="56fc7-164">Open in Visual Studio **Web.Release.config** in uw project.</span><span class="sxs-lookup"><span data-stu-id="56fc7-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="56fc7-165">Voeg de volgende XML in de `<configuration>` labelen en vervang de waarde van de sleutel met uw publish web-app-URL.</span><span class="sxs-lookup"><span data-stu-id="56fc7-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="56fc7-166">Wanneer u bent klaar, hebt u twee RP id's die worden geconfigureerd in uw project, één voor uw omgeving voor foutopsporing in Visual Studio en één voor de gepubliceerde web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="56fc7-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="56fc7-167">Stelt u een vertrouwensrelatie RP voor elk van deze twee omgevingen in AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="56fc7-168">Tijdens de foutopsporing, instellingen voor de app in web.config-bestand worden gebruikt om uw **Debug** configuratie werken met AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="56fc7-169">Wanneer deze wordt gepubliceerd (standaard de **Release** configuratie wordt gepubliceerd), een getransformeerde Web.config waarin de wijzigingen van de app-instelling in Web.Release.config wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="56fc7-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="56fc7-170">Als u wilt koppelen van de gepubliceerde web-app in Azure om het foutopsporingsprogramma (dat wil zeggen moet u de symbolen foutopsporing van uw code in de gepubliceerde web-app uploaden), kunt u een kloon van de configuratie van de foutopsporing voor het opsporen van Azure, maar met een eigen aangepaste Web.config-transformatie (bijvoorbeeld Web.AzureDebug.config) die gebruikmaakt van de appinstellingen van Web.Release.config maken.</span><span class="sxs-lookup"><span data-stu-id="56fc7-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="56fc7-171">Hiermee kunt u de configuratie van een statische onderhouden in de verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="56fc7-172">Vertrouwensrelaties met relying party's in AD FS-beheer configureren</span><span class="sxs-lookup"><span data-stu-id="56fc7-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="56fc7-173">Nu moet u een vertrouwensrelatie RP in AD FS-beheer configureren voordat u kunt de voorbeeldtoepassing en daadwerkelijk met AD FS verifiëren.</span><span class="sxs-lookup"><span data-stu-id="56fc7-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="56fc7-174">U moet twee afzonderlijke RP-vertrouwensrelaties, één voor uw omgeving voor foutopsporing en één voor de gepubliceerde web-app instellen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="56fc7-175">Zorg ervoor dat u de volgende stappen herhalen voor zowel uw omgevingen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="56fc7-176">Aanmelden met referenties op waarmee de rights management in AD FS hebt op uw AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="56fc7-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="56fc7-177">Open AD FS-beheer.</span><span class="sxs-lookup"><span data-stu-id="56fc7-177">Open AD FS Management.</span></span> <span data-ttu-id="56fc7-178">Met de rechtermuisknop op **AD FS\Trusted Relationships\Relying Party-vertrouwensrelaties** en selecteer **Relying Party Trust toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="56fc7-179">In de **gegevensbron selecteren** pagina **gegevens over de relying party handmatig invoeren**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="56fc7-180">In de **weergavenaam opgeven** pagina, typ een weergavenaam voor de toepassing en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="56fc7-181">In de **Protocol kiezen** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="56fc7-182">In de **certificaat configureren** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56fc7-183">Omdat u moet worden gebruikt voor HTTPS al, is versleuteld tokens zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="56fc7-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="56fc7-184">Als u zeker versleutelen tokens van AD FS op deze pagina wilt, moet u ook logica tokenontsleuteling toevoegen in uw code.</span><span class="sxs-lookup"><span data-stu-id="56fc7-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="56fc7-185">Zie voor meer informatie [handmatig OWIN WS-Federation-middleware configureren en het accepteren van tokens versleuteld](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="56fc7-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="56fc7-186">Voordat u naar de volgende stap verplaatst, moet u een stukje informatie van uw Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="56fc7-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="56fc7-187">Noteer in de Projecteigenschappen de **SSL URL** van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="56fc7-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="56fc7-188">AD FS-beheer, weer de **URL configureren** pagina van de **toevoegen Wizard Relying Party Trust**, selecteer **ondersteuning voor de WS-Federation Passive protocol inschakelen** en typt u de SSL-URL van uw Visual Studio-project dat u in de vorige stap hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="56fc7-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="56fc7-189">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="56fc7-190">URL geeft aan waar de client verzenden nadat een verificatie geslaagde.</span><span class="sxs-lookup"><span data-stu-id="56fc7-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="56fc7-191">Voor de omgeving foutopsporing moet <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="56fc7-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="56fc7-192">Voor de gepubliceerde web-app, moet de app-URL.</span><span class="sxs-lookup"><span data-stu-id="56fc7-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="56fc7-193">In de **id's configureren** pagina, controleert u of de SSL-URL van uw project al is vermeld en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="56fc7-194">Klik op **volgende** helemaal tot aan het einde van de wizard met de standaardselecties.</span><span class="sxs-lookup"><span data-stu-id="56fc7-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56fc7-195">In App_Start\Startup.Auth.cs van Visual Studio-project deze id wordt vergeleken met de waarde van <code>WsFederationAuthenticationOptions.Wtrealm</code> tijdens federatieve verificatie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="56fc7-196">Standaard wordt de URL van de toepassing van de vorige stap toegevoegd als een RP-id.</span><span class="sxs-lookup"><span data-stu-id="56fc7-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="56fc7-197">U bent nu klaar om de RP-toepassingen configureren voor uw project in AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="56fc7-198">Vervolgens configureert u deze toepassing verzenden van de claims die nodig is voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="56fc7-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="56fc7-199">De **Claimregels bewerken** dialoogvenster wordt standaard voor u geopend aan het einde van de wizard zodat u meteen kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="56fc7-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="56fc7-200">Laten we Configureer ten minste de volgende claims (met schema's tussen haakjes):</span><span class="sxs-lookup"><span data-stu-id="56fc7-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="56fc7-201">Naam van (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - door ASP.NET hydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="56fc7-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="56fc7-202">UPN (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn -) gebruikt als unieke identificatie van gebruikers in de organisatie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="56fc7-203">Groepslidmaatschappen als (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - rollen kan worden gebruikt met `[Authorize(Roles="role1, role2,...")]` decoration domeincontrollers/acties autoriseren.</span><span class="sxs-lookup"><span data-stu-id="56fc7-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="56fc7-204">Deze aanpak mogelijk in werkelijkheid is niet de meeste zodat voor rolautorisatie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="56fc7-205">Als uw AD-gebruikers tot honderden beveiligingsgroepen behoren, worden ze honderden rolclaims in het SAML-token.</span><span class="sxs-lookup"><span data-stu-id="56fc7-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="56fc7-206">Er is een alternatieve methode voor het verzenden van een claim één rol voor voorwaardelijk afhankelijk van het lidmaatschap van de gebruiker in een bepaalde groep.</span><span class="sxs-lookup"><span data-stu-id="56fc7-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="56fc7-207">Maar je we Houd het eenvoudig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="56fc7-208">Gebruikersnaam (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - kunnen worden gebruikt voor validatie antivirusprogramma kunnen worden vervalst.</span><span class="sxs-lookup"><span data-stu-id="56fc7-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="56fc7-209">Zie voor meer informatie over het maken van werken met ter voorkoming validatie de **line-of-business-functionaliteit toevoegen** sectie van [een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="56fc7-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="56fc7-210">De claimtypen die u wilt configureren voor uw toepassing wordt bepaald door de behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="56fc7-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="56fc7-211">Voor de lijst met claims die worden ondersteund door Azure Active Directory-toepassingen (dat wil zeggen RP-vertrouwensrelaties), bijvoorbeeld zien [ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="56fc7-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="56fc7-212">Klik in het dialoogvenster Claimregels bewerken op **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="56fc7-213">De naam, UPN en rol claims configureren zoals wordt weergegeven in de schermafbeelding en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="56fc7-214">Maak vervolgens een tijdelijke naam ID claim in met behulp van de stappen uitgelegd [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="56fc7-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="56fc7-215">Klik op **regel toevoegen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="56fc7-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="56fc7-216">Selecteer **Claims verzenden met een aangepaste regel** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="56fc7-217">Plak de volgende regel taal in de **aangepaste regel** vak en de naam van de regel **Per sessie-id** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="56fc7-218">Uw aangepaste regel moet eruitzien als in deze schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="56fc7-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="56fc7-219">Klik op **regel toevoegen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="56fc7-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="56fc7-220">Selecteer **een binnenkomende Claim transformeren** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="56fc7-221">De regel configureren zoals wordt weergegeven in de schermafbeelding (met het claimtype die u hebt gemaakt in de aangepaste regel) en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="56fc7-222">Zie voor gedetailleerde informatie over de stappen voor de tijdelijke naam-ID claim [identificaties voor kolomnamen in SAML asserties](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="56fc7-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="56fc7-223">Klik op **toepassen** in de **Claimregels bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="56fc7-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="56fc7-224">Nu ziet er in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="56fc7-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="56fc7-225">Zorg ervoor dat u deze stappen herhalen voor uw omgeving voor foutopsporing en de gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="56fc7-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="56fc7-226">Federatieve verificatie voor uw toepassing testen</span><span class="sxs-lookup"><span data-stu-id="56fc7-226">Test federated authentication for your application</span></span>
<span data-ttu-id="56fc7-227">U bent klaar voor het testen van uw toepassing verificatielogica op basis van AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="56fc7-228">Ik heb een testgebruiker op die bij een testgroep in Active Directory (AD hoort) in de AD FS-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="56fc7-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="56fc7-229">Als u wilt testen verificatie in het foutopsporingsprogramma, hoeft u nu type is `F5`.</span><span class="sxs-lookup"><span data-stu-id="56fc7-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="56fc7-230">Als u testen verificatie in de gepubliceerde web-app wilt, gaat u naar de URL.</span><span class="sxs-lookup"><span data-stu-id="56fc7-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="56fc7-231">Nadat de webtoepassing is geladen, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="56fc7-232">U krijgt nu een dialoogvenster voor aanmelding of de aanmeldingspagina afgehandeld door AD FS is afhankelijk van de verificatiemethode die wordt gekozen door AD FS.</span><span class="sxs-lookup"><span data-stu-id="56fc7-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="56fc7-233">Hier volgt ik in Internet Explorer 11 krijgen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="56fc7-234">Zodra u aanmelden als gebruiker in het AD-domein van de AD FS-implementatie, u ziet nu de startpagina opnieuw met **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="56fc7-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="56fc7-235">in de hoek.</span><span class="sxs-lookup"><span data-stu-id="56fc7-235">in the corner.</span></span> <span data-ttu-id="56fc7-236">Hier volgt krijg ik.</span><span class="sxs-lookup"><span data-stu-id="56fc7-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="56fc7-237">U hebt tot nu toe is voltooid op de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="56fc7-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="56fc7-238">Uw toepassing heeft de AD FS is bereikt en een overeenkomende RP-id is gevonden in de AD FS-database</span><span class="sxs-lookup"><span data-stu-id="56fc7-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="56fc7-239">AD FS is geverifieerd een AD-gebruiker en een omleiding die u terug naar de startpagina van de toepassing</span><span class="sxs-lookup"><span data-stu-id="56fc7-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="56fc7-240">AD FS als verzonden de naamclaim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) voor uw toepassing, zoals aangegeven door het feit dat de gebruikersnaam wordt weergegeven in de hoek.</span><span class="sxs-lookup"><span data-stu-id="56fc7-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="56fc7-241">Als de claim ontbreekt, u zou hebben gezien **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="56fc7-242">Als u Views\Shared bekijkt\_LoginPartial.cshtml, vindt u die gebruikmaakt van `User.Identity.Name` om de naam van de gebruiker weer te geven.</span><span class="sxs-lookup"><span data-stu-id="56fc7-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="56fc7-243">Zoals gezegd, als de naamclaim van de geverifieerde gebruiker beschikbaar in het SAML-token is, hydrates ASP.NET deze eigenschap aan.</span><span class="sxs-lookup"><span data-stu-id="56fc7-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="56fc7-244">Overzicht van de claims die worden verzonden door AD FS een onderbrekingspunt in Controllers\HomeController.cs, te plaatsen in de Index-actiemethode.</span><span class="sxs-lookup"><span data-stu-id="56fc7-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="56fc7-245">Nadat de gebruiker is geverifieerd, Inspecteer de `System.Security.Claims.Current.Claims` verzameling.</span><span class="sxs-lookup"><span data-stu-id="56fc7-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="56fc7-246">Autoriseren van gebruikers voor specifieke domeincontrollers of acties</span><span class="sxs-lookup"><span data-stu-id="56fc7-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="56fc7-247">Aangezien u groepslidmaatschappen als rolclaims in uw configuratie van de vertrouwensrelatie RP hebt opgenomen, kunt u nu gebruiken ze rechtstreeks in de `[Authorize(Roles="...")]` decoration voor domeincontrollers en acties.</span><span class="sxs-lookup"><span data-stu-id="56fc7-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="56fc7-248">U kunt specifieke functies voor toegang tot elke actie autoriseren in een line-of-business-toepassing met het patroon maken, lezen, bijwerken, verwijderen (CRUD).</span><span class="sxs-lookup"><span data-stu-id="56fc7-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="56fc7-249">Op dit moment wordt u alleen deze functie op de bestaande Home controller uitproberen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="56fc7-250">Open Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="56fc7-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="56fc7-251">Opmaken de `About` en `Contact` actiemethoden vergelijkbaar met de volgende code, met security groepslidmaatschappen dat de geverifieerde gebruiker heeft.</span><span class="sxs-lookup"><span data-stu-id="56fc7-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="56fc7-252">Nadat ik toegevoegd **gebruiker testen** naar **testgroep** in mijn AD FS-testomgeving ik testgroep gebruik autorisatie testen op `About`.</span><span class="sxs-lookup"><span data-stu-id="56fc7-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="56fc7-253">Voor `Contact`, test ik het negatieve geval van **Domeinadministrators**toe aan die **gebruiker testen** behoort niet toe.</span><span class="sxs-lookup"><span data-stu-id="56fc7-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="56fc7-254">Het foutopsporingsprogramma start door te typen `F5` en meld u aan en klik vervolgens op **over**.</span><span class="sxs-lookup"><span data-stu-id="56fc7-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="56fc7-255">U moet nu bekijkt de `~/About/Index` pagina geslaagd, als de geverifieerde gebruiker is gemachtigd voor deze actie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="56fc7-256">Klik nu op **Contact**, die in mijn geval dienen niet toe te staan **testgebruiker** voor de actie.</span><span class="sxs-lookup"><span data-stu-id="56fc7-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="56fc7-257">Echter, de browser wordt omgeleid naar AD FS, die uiteindelijk ziet u dit bericht:</span><span class="sxs-lookup"><span data-stu-id="56fc7-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="56fc7-258">Als u deze fout in Logboeken op de AD FS-server onderzoeken, ziet u dit bericht van uitzondering:</span><span class="sxs-lookup"><span data-stu-id="56fc7-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="56fc7-259">De reden voor deze fout is dat standaard MVC een 401 niet geautoriseerd retourneert wanneer rollen van een gebruiker bent niet gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="56fc7-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="56fc7-260">Dit activeert een aanvraag herauthenticatie id-provider (AD FS).</span><span class="sxs-lookup"><span data-stu-id="56fc7-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="56fc7-261">Omdat de gebruiker al is geverifieerd, wordt AD FS retourneert op dezelfde pagina, vervolgens geeft u een andere 401, een lus omleiding maken.</span><span class="sxs-lookup"><span data-stu-id="56fc7-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="56fc7-262">Overschrijft u de AuthorizeAttribute `HandleUnauthorizedRequest` methode met eenvoudige logica voor het weergeven van iets die zinvol in plaats van de lus omleiding u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="56fc7-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="56fc7-263">Maak een bestand in het project met de naam AuthorizeAttribute.cs en plak de volgende code in deze.</span><span class="sxs-lookup"><span data-stu-id="56fc7-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="56fc7-264">De onderdrukking code verzendt een HTTP 403 (verboden) in plaats van 401 HTTP-(niet-geautoriseerd) in geverifieerde maar niet-geautoriseerde gevallen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="56fc7-265">Voer het foutopsporingsprogramma opnieuw met `F5`.</span><span class="sxs-lookup"><span data-stu-id="56fc7-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="56fc7-266">Te klikken op **Contact** nu een meer informatieve (die mogelijk zwartwitprinter) foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="56fc7-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="56fc7-267">De toepassing publiceren in Azure App Service Web Apps opnieuw en het gedrag van de live-toepassing te testen.</span><span class="sxs-lookup"><span data-stu-id="56fc7-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="56fc7-268">Verbinding maken met on-premises gegevens</span><span class="sxs-lookup"><span data-stu-id="56fc7-268">Connect to on-premises data</span></span>
<span data-ttu-id="56fc7-269">Een reden zou willen implementeren van uw line-of-business-toepassing met AD FS in plaats van Azure Active Directory is problemen met de compatibiliteit met het up-to-date houden organisatie gegevens uit de lokale.</span><span class="sxs-lookup"><span data-stu-id="56fc7-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="56fc7-270">Dit kan ook betekenen dat uw web-app in Azure toegang lokale databases, tot moet omdat u niet mag gebruiken [SQL-Database](/services/sql-database/) als de gegevenslaag voor uw web-apps.</span><span class="sxs-lookup"><span data-stu-id="56fc7-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="56fc7-271">Azure App Service Web Apps biedt ondersteuning voor toegang tot lokale databases met twee benaderingen: [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [virtuele netwerken](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="56fc7-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="56fc7-272">Zie voor meer informatie [VNET met behulp van integratie en hybride verbindingen met Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="56fc7-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="56fc7-273">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="56fc7-273">Further resources</span></span>
* [<span data-ttu-id="56fc7-274">Verificatie met de on-premises Active Directory in uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="56fc7-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="56fc7-275">Een Azure line-of-business-app maken met Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="56fc7-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="56fc7-276">De optie voor organisatie-verificatie in de On-Premises (AD FS) gebruiken met ASP.NET in Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="56fc7-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="56fc7-277">Migreren van een webproject VS2013 van WIF naar Katana</span><span class="sxs-lookup"><span data-stu-id="56fc7-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="56fc7-278">Overzicht van Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="56fc7-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="56fc7-279">1.1 van WS-Federation-specificatie</span><span class="sxs-lookup"><span data-stu-id="56fc7-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

