---
title: Gebruikersverificatie voor API-Apps in Azure App Service | Microsoft Docs
description: Informatie over het beveiligen van een API-app in Azure App Service doordat alleen toegang tot geverifieerde gebruikers.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="f94d9-103">Gebruikersverificatie voor API-Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f94d9-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="f94d9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f94d9-104">Overview</span></span>
<span data-ttu-id="f94d9-105">In dit artikel laat zien hoe een Azure-API-app beveiligen zodat alleen geverifieerde gebruikers kunnen worden aanroepen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="f94d9-106">Het artikel wordt ervan uitgegaan dat u hebt gelezen de [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="f94d9-107">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="f94d9-107">You'll learn:</span></span>

* <span data-ttu-id="f94d9-108">Klik hier voor meer informatie over het configureren van een verificatieprovider, met details voor Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f94d9-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="f94d9-109">Een beveiligde API-app gebruiken met behulp van de [Active Directory Authentication Library (ADAL) voor JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span><span class="sxs-lookup"><span data-stu-id="f94d9-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="f94d9-110">Het artikel bestaat uit twee gedeelten:</span><span class="sxs-lookup"><span data-stu-id="f94d9-110">The article contains two sections:</span></span>

* <span data-ttu-id="f94d9-111">De [gebruikersverificatie configureren in Azure App Service](#authconfig) .NET, Node.js, met inbegrip van sectie wordt uitgelegd in het algemeen het configureren van gebruikersverificatie voor API Apps en is evenveel van toepassing op alle frameworks die worden ondersteund door App Service en Java.</span><span class="sxs-lookup"><span data-stu-id="f94d9-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="f94d9-112">Beginnen met de [u doorgaat met de .NET API Apps-zelfstudies](#tutorialstart) sectie, het artikel begeleidt u bij het configureren van een voorbeeldtoepassing met een .NET-back-end en een AngularJS-front-end dat gebruikmaakt van Azure Active Directory voor gebruiker -verificatie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <span data-ttu-id="f94d9-113"><a id="authconfig"></a>Verificatie van de gebruiker in Azure App Service configureren</span><span class="sxs-lookup"><span data-stu-id="f94d9-113"><a id="authconfig"></a> How to configure user authentication in Azure App Service</span></span>
<span data-ttu-id="f94d9-114">Deze sectie bevat algemene instructies die betrekking hebben op elke API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-114">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="f94d9-115">Voor specifieke stappen voor de voorbeeldtoepassing te doen lijst-.NET, gaat u naar [u doorgaat met de zelfstudies .NET aan de slag](#tutorialstart).</span><span class="sxs-lookup"><span data-stu-id="f94d9-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="f94d9-116">In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u wilt beveiligen, vinden de **functies** sectie en klik vervolgens op  **Verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f94d9-118">In de **verificatie / autorisatie** blade, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-118">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f94d9-119">Selecteer een van de opties uit de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f94d9-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="f94d9-120">Als u wilt dat alleen geverifieerde aanroepen naar uw API-app te bereiken, kies een van de **Meld u aan met...**  opties.</span><span class="sxs-lookup"><span data-stu-id="f94d9-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span></span> <span data-ttu-id="f94d9-121">Deze optie kunt u de API-app beveiligen zonder het schrijven van code die in deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f94d9-121">This option enables you to protect the API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="f94d9-122">Als u wilt dat alle aanroepen voor het bereiken van uw API-app, kiest u **aanvraag toestaan (geen actie)**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="f94d9-123">U kunt deze optie gebruiken om niet-geverifieerde aanroepfuncties een keuze uit verificatieproviders leiden.</span><span class="sxs-lookup"><span data-stu-id="f94d9-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span></span> <span data-ttu-id="f94d9-124">Met deze optie hebt u code schrijven om de verwerking van autorisatie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-124">With this option you have to write code to handle authorization.</span></span>
     
     <span data-ttu-id="f94d9-125">Zie [Verificatie en autorisatie voor API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="f94d9-126">Selecteer een of meer van de **verificatieproviders**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-126">Select one or more of the **Authentication Providers**.</span></span>
   
    <span data-ttu-id="f94d9-127">De afbeelding toont keuzes waarbij alle aanroepfuncties moet worden geverifieerd door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f94d9-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span></span>
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="f94d9-129">Als u een verificatieprovider kiest, de portal wordt weergegeven van een configuratie-blade voor die provider.</span><span class="sxs-lookup"><span data-stu-id="f94d9-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="f94d9-130">Zie voor gedetailleerde instructies met uitleg over het configureren van de verificatie-provider configuratie blades [het configureren van uw App Service-toepassing voor het gebruik van Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="f94d9-131">(De koppeling gaat u naar een artikel over Azure AD, maar het artikel zelf bevat tabbladen die een koppeling naar artikelen voor de authenticatieproviders.)</span><span class="sxs-lookup"><span data-stu-id="f94d9-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span></span>
5. <span data-ttu-id="f94d9-132">Wanneer u met de blade verificatie provider configuratie bent klaar, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-132">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="f94d9-133">In de **verificatie / autorisatie** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-133">In the **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="f94d9-134">Wanneer dit wordt gedaan, wordt alle API-aanroepen in App Service geverifieerd voordat ze de API-app bereiken.</span><span class="sxs-lookup"><span data-stu-id="f94d9-134">When this is done, App Service authenticates all API calls before they reach the API app.</span></span> <span data-ttu-id="f94d9-135">De verificatieservices werkt hetzelfde voor alle talen die App-service wordt ondersteund, waaronder .NET, Node.js en Java.</span><span class="sxs-lookup"><span data-stu-id="f94d9-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="f94d9-136">Als u geverifieerde API-aanroepen, bevat de aanroeper de verificatieprovider OAuth 2.0-bearer-token in autorisatie-header van HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span></span> <span data-ttu-id="f94d9-137">Het token kan worden verkregen met behulp van de verificatieprovider SDK.</span><span class="sxs-lookup"><span data-stu-id="f94d9-137">The token can be acquired by using the authentication provider's SDK.</span></span>

## <span data-ttu-id="f94d9-138"><a id="tutorialstart"></a>U kunt doorgaan de zelfstudies .NET API-Apps</span><span class="sxs-lookup"><span data-stu-id="f94d9-138"><a id="tutorialstart"></a> Continuing the .NET API Apps tutorials</span></span>
<span data-ttu-id="f94d9-139">Als u de zelfstudies Node.js of Java voor API-apps volgt, gaat u naar het volgende artikel [principal verificatie van de service voor API-apps](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="f94d9-140">Als u de .NET-zelfstudie-reeks voor API-apps volgt en al de voorbeeldtoepassing hebben geïmplementeerd zoals beschreven in de [eerste](app-service-api-dotnet-get-started.md) en [tweede](app-service-api-cors-consume-javascript.md) zelfstudies, gaat u verder met de [instellen verificatie in App Service en Azure AD](#azureauth) sectie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="f94d9-141">Als u Volg deze zelfstudie wilt zonder tussenkomst van de eerste en tweede zelfstudies, doet u de volgende stappen die wordt uitgelegd hoe u aan de slag met behulp van een geautomatiseerd proces voor het implementeren van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f94d9-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="f94d9-142">De volgende stappen kunnen u naar het hetzelfde beginpunt als wanneer u de eerste twee zelfstudies, met één uitzondering is: Visual Studio al weet niet welk web-app of API-app die elk project wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f94d9-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="f94d9-143">Dit betekent dat u hebt geen exacte instructies in deze zelfstudie waarin wordt uitgelegd hoe om te implementeren op de juiste doelen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span></span> <span data-ttu-id="f94d9-144">Als u niet vertrouwd bent met hoe de implementatiestappen zelf doen, is het beter te volgen van de zelfstudie reeks van de [eerste zelfstudie](app-service-api-dotnet-get-started.md) dan beginnen met dit implementatieproces geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="f94d9-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="f94d9-145">Zorg dat u alle vereisten die worden vermeld in de [eerste zelfstudie](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="f94d9-146">Naast de vereisten die worden vermeld, deze zelfstudies verificatie wordt ervan uitgegaan dat u hebt gewerkt met App Service-web-apps en API-apps in Visual Studio en de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f94d9-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span></span>
2. <span data-ttu-id="f94d9-147">Klik op de **implementeren in Azure** knop in de [To Do List voorbeeld opslagplaats Leesmij-bestand](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) om de API-apps en de web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f94d9-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span></span> <span data-ttu-id="f94d9-148">Noteer de Azure-resourcegroep die wordt gemaakt, zoals u dit kunt later om web-app en de namen van de API-app te zoeken.</span><span class="sxs-lookup"><span data-stu-id="f94d9-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span></span>
3. <span data-ttu-id="f94d9-149">Downloaden of te klonen de [To Do List voorbeeld opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) ophalen van de code die u met lokaal in Visual Studio werkt.</span><span class="sxs-lookup"><span data-stu-id="f94d9-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span></span>

## <span data-ttu-id="f94d9-150"><a id="azureauth"></a>Verificatie in App Service en Azure AD instellen</span><span class="sxs-lookup"><span data-stu-id="f94d9-150"><a id="azureauth"></a> Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="f94d9-151">U hebt nu de toepassing die wordt uitgevoerd in Azure App Service zonder dat gebruikers worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="f94d9-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="f94d9-152">In deze sectie kunt u verificatie toevoegt als volgt u de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="f94d9-152">In this section you add authentication by doing the following tasks:</span></span>

* <span data-ttu-id="f94d9-153">App Service configureren voor Azure Active Directory (Azure AD) verificatie vereisen voor het aanroepen van de middelste laag API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span></span>
* <span data-ttu-id="f94d9-154">Maak een Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f94d9-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="f94d9-155">De Azure AD-toepassing de bearer-token na aanmelding verzenden naar de AngularJS-front-end configureren.</span><span class="sxs-lookup"><span data-stu-id="f94d9-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span></span> 

<span data-ttu-id="f94d9-156">Als u problemen ondervindt tijdens de zelfstudie aanwijzingen, raadpleegt u de [probleemoplossing](#troubleshooting) sectie aan het einde van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a><span data-ttu-id="f94d9-157">Verificatie voor de middelste laag API-app configureren</span><span class="sxs-lookup"><span data-stu-id="f94d9-157">Configure authentication for the middle tier API app</span></span>
1. <span data-ttu-id="f94d9-158">In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u hebt gemaakt voor het project ToDoListAPI, vinden de **functies** sectie en klik vervolgens op  **Verificatie / autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f94d9-160">In de **verificatie / autorisatie** blade, klikt u op **op**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-160">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f94d9-161">In de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="f94d9-162">Deze optie zorgt ervoor dat er geen aanvragen voor unauathenticated wordt toegang heeft tot de API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-162">This option ensures that no unauathenticated requests will reach the API app.</span></span> 
4. <span data-ttu-id="f94d9-163">Onder **verificatieproviders**, klikt u op **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="f94d9-165">In de **Azure Active Directory-instellingen** blade, klikt u op **Express**</span><span class="sxs-lookup"><span data-stu-id="f94d9-165">In the **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure portal-verificatie/autorisatie Express optie](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="f94d9-167">Met de **Express** optie App Service kunt automatisch een Azure AD-toepassing maken in uw Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span><span class="sxs-lookup"><span data-stu-id="f94d9-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="f94d9-168">U hoeft te maken van een tenant omdat elke Azure-account automatisch een heeft.</span><span class="sxs-lookup"><span data-stu-id="f94d9-168">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="f94d9-169">Onder **beheermodus**, klikt u op **nieuwe AD-App maken** als deze niet al is geselecteerd en Let op de waarde die in de **App maken** tekstvak; u moet deze AAD opzoeken later toepassing in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f94d9-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span></span>
   
    ![Azure-portal Azure AD-instellingen](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="f94d9-171">Azure maakt automatisch een Azure AD-toepassing met de naam van de aangegeven in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="f94d9-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="f94d9-172">Standaard is de Azure AD-toepassing naam hetzelfde zijn als de API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-172">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="f94d9-173">Als u liever, kunt u een andere naam.</span><span class="sxs-lookup"><span data-stu-id="f94d9-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="f94d9-174">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-174">Click **OK**.</span></span>
8. <span data-ttu-id="f94d9-175">In de **verificatie / autorisatie** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-175">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="f94d9-177">Alleen gebruikers in uw Azure AD-tenant kunnen nu de API-app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-177">Now only users in your Azure AD tenant can call the API app.</span></span>

### <a name="optional-test-the-api-app"></a><span data-ttu-id="f94d9-178">Optioneel: Het testen van de API-app</span><span class="sxs-lookup"><span data-stu-id="f94d9-178">Optional: Test the API app</span></span>
1. <span data-ttu-id="f94d9-179">Ga in een browser naar de URL van de API-app: in de **API-app** blade in de Azure-portal klikt u op de koppeling onder **URL**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span>  
   
    <span data-ttu-id="f94d9-180">U wordt omgeleid naar een aanmeldingsscherm omdat niet-geverifieerde aanvragen zijn niet toegestaan voor het bereiken van de API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span>
   
    <span data-ttu-id="f94d9-181">Als uw browser gaat naar de pagina 'is gemaakt', kan al de browser worden geregistreerd op--in dat geval open een InPrivate- of Incognito-venster en Ga naar de API-app-URL.</span><span class="sxs-lookup"><span data-stu-id="f94d9-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span></span>
2. <span data-ttu-id="f94d9-182">Meld u aan met referenties voor een gebruiker in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="f94d9-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="f94d9-183">Wanneer u bent aangemeld, wordt de pagina 'is gemaakt' in de browser weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f94d9-183">When you're logged on, the "successfully created" page appears in the browser.</span></span>
3. <span data-ttu-id="f94d9-184">Sluit de browser.</span><span class="sxs-lookup"><span data-stu-id="f94d9-184">Close the browser.</span></span>

### <a name="configure-the-azure-ad-application"></a><span data-ttu-id="f94d9-185">De toepassing Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f94d9-185">Configure the Azure AD application</span></span>
<span data-ttu-id="f94d9-186">Wanneer u Azure AD-verificatie hebt geconfigureerd, wordt in App Service een Azure AD-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f94d9-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="f94d9-187">Toepassing is standaard ingesteld op de nieuwe Azure AD geconfigureerd voor de bearer-token naar de API-app-URL.</span><span class="sxs-lookup"><span data-stu-id="f94d9-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span></span> <span data-ttu-id="f94d9-188">In deze sectie configureert u de Azure AD-toepassing voor de bearer-token naar de AngularJS front-end in plaats van rechtstreeks op de middelste laag API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span></span> <span data-ttu-id="f94d9-189">De AngularJS-front-end stuurt het token naar de API-app wanneer de API-app roept.</span><span class="sxs-lookup"><span data-stu-id="f94d9-189">The AngularJS front end will send the token to the API app when it calls the API app.</span></span>

> [!NOTE]
> <span data-ttu-id="f94d9-190">Bewaren van het proces als eenvoudig mogelijk, deze zelfstudie maakt gebruik van een enkele Azure AD-toepassing voor zowel de front-end- en het midden gegevenslaag vormt API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span></span> <span data-ttu-id="f94d9-191">Een andere optie is het gebruik van twee Azure AD-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-191">Another option is to use two Azure AD applications.</span></span> <span data-ttu-id="f94d9-192">In dat geval moet u de front-end Azure AD-toepassing toestemming om aan te roepen Azure AD-toepassing voor de middelste laag geven.</span><span class="sxs-lookup"><span data-stu-id="f94d9-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span></span> <span data-ttu-id="f94d9-193">Deze aanpak meerdere toepassingen, krijgt u meer gedetailleerde controle over machtigingen voor elke laag.</span><span class="sxs-lookup"><span data-stu-id="f94d9-193">This multi-application approach would give you more granular control over permissions to each tier.</span></span>
> 
> 

1. <span data-ttu-id="f94d9-194">In de [klassieke Azure-portal](https://manage.windowsazure.com/), gaat u naar **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
   
   <span data-ttu-id="f94d9-195">U moet de klassieke portal gebruiken, omdat bepaalde Azure Active Directory-instellingen die u toegang tot moet nog niet beschikbaar in de huidige Azure-portal zijn.</span><span class="sxs-lookup"><span data-stu-id="f94d9-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span></span>
2. <span data-ttu-id="f94d9-196">Op de **Directory** tabblad, klikt u op uw AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="f94d9-196">On the **Directory** tab, click your AAD tenant.</span></span>
   
   ![Azure AD in de klassieke portal](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="f94d9-198">Klik op **toepassingen > Mijn bedrijf eigenaar is van toepassingen**, en klik vervolgens op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="f94d9-198">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
   
   <span data-ttu-id="f94d9-199">Mogelijk moet u ook Vernieuw de pagina overzicht van de nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="f94d9-199">You might also have to refresh the page to see the new application.</span></span>
4. <span data-ttu-id="f94d9-200">Klik in de lijst met toepassingen op de naam van de gebruiker die Azure voor u gemaakt wanneer u verificatie is ingeschakeld voor uw API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Op het tabblad Azure AD-toepassingen](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="f94d9-202">Klik op **Configureren**</span><span class="sxs-lookup"><span data-stu-id="f94d9-202">Click **Configure**.</span></span>
   
   ![Tabblad met Azure AD configureren](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="f94d9-204">Stel **aanmeldings-URL** op de URL voor uw AngularJS-web-app, geen afsluitende slash.</span><span class="sxs-lookup"><span data-stu-id="f94d9-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f94d9-205">Bijvoorbeeld: https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f94d9-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![Aanmeldings-URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="f94d9-207">Stel **antwoord-URL** op de URL voor uw web-app geen afsluitende slash.</span><span class="sxs-lookup"><span data-stu-id="f94d9-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f94d9-208">Bijvoorbeeld: https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f94d9-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="f94d9-209">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-209">Click **Save**.</span></span>
   
   ![Antwoord-URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="f94d9-211">Klik onder aan de pagina op **beheren manifest > downloaden manifest**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span></span>
   
   ![Downloaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="f94d9-213">Download het bestand naar een locatie waar u het kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="f94d9-213">Download the file to a location where you can edit it.</span></span>
11. <span data-ttu-id="f94d9-214">Zoek in het gedownloade manifestbestand voor het `oauth2AllowImplicitFlow` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f94d9-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="f94d9-215">Wijzig de waarde van deze eigenschap van `false` naar `true`, en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="f94d9-215">Change the value of this property from `false` to `true`, and then save the file.</span></span>
    
    <span data-ttu-id="f94d9-216">Deze instelling is vereist voor toegang tot een JavaScript-toepassing voor één pagina.</span><span class="sxs-lookup"><span data-stu-id="f94d9-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="f94d9-217">Kan de Oauth 2.0-bearer-token wordt in het URL-fragment geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f94d9-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span></span>
12. <span data-ttu-id="f94d9-218">Klik op **beheren manifest > uploaden manifest**, en upload het bestand dat u in de vorige stap hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f94d9-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span></span>
    
    ![Uploaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="f94d9-220">Kopieer de **Client-ID** waarde en sla dit op een locatie kunt u dit uit later downloaden.</span><span class="sxs-lookup"><span data-stu-id="f94d9-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-the-todolistangular-project-to-use-authentication"></a><span data-ttu-id="f94d9-221">Configureren van het project ToDoListAngular om verificatie te gebruiken</span><span class="sxs-lookup"><span data-stu-id="f94d9-221">Configure the ToDoListAngular project to use authentication</span></span>
<span data-ttu-id="f94d9-222">In deze sectie wijzigt u de AngularJS-front-end dat gebruikmaakt van Active Directory Authentication Library (ADAL) voor JS te verkrijgen van een bearer-token voor de aangemelde gebruiker van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f94d9-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span></span> <span data-ttu-id="f94d9-223">De code neemt het token in HTTP-aanvragen verzonden naar de middelste laag, zoals wordt weergegeven in het volgende diagram.</span><span class="sxs-lookup"><span data-stu-id="f94d9-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span></span> 

![Gebruiker-verificatiediagram](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="f94d9-225">De volgende wijzigingen aanbrengen in bestanden in het project ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="f94d9-225">Make the following changes to files in the ToDoListAngular project.</span></span>

1. <span data-ttu-id="f94d9-226">Open de *index.cshtml* bestand.</span><span class="sxs-lookup"><span data-stu-id="f94d9-226">Open the *index.cshtml* file.</span></span>
2. <span data-ttu-id="f94d9-227">Verwijder de opmerkingen in de regels die verwijzen naar de Active Directory Authentication Library (ADAL) voor JS scripts.</span><span class="sxs-lookup"><span data-stu-id="f94d9-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="f94d9-228">Open de *app/scripts/app.js* bestand.</span><span class="sxs-lookup"><span data-stu-id="f94d9-228">Open the *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="f94d9-229">Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.</span><span class="sxs-lookup"><span data-stu-id="f94d9-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="f94d9-230">Deze wijziging verwijst naar de ADAL JS verificatieprovider en biedt configuratiewaarden aan.</span><span class="sxs-lookup"><span data-stu-id="f94d9-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span></span> <span data-ttu-id="f94d9-231">In de volgende stappen stelt u de configuratiewaarden voor uw API-app en Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f94d9-231">In the following steps you set the configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="f94d9-232">In de code die Hiermee stelt u de `endpoints` variabele, de API-URL naar de URL van de API-app instellen dat u voor het project ToDoListAPI gemaakt en de Azure AD-toepassings-ID ingesteld op de client-ID die u hebt gekopieerd uit de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f94d9-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span></span>
   
    <span data-ttu-id="f94d9-233">De code is nu vergelijkbaar met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f94d9-233">The code is now similar to the following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="f94d9-234">In de aanroep naar `adalProvider.init`stelt `tenant` aan de tenantnaam van uw en `clientId` op dezelfde waarde die u hebt gebruikt in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="f94d9-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span></span>
   
    <span data-ttu-id="f94d9-235">De code is nu vergelijkbaar met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f94d9-235">The code is now similar to the following example.</span></span>
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    <span data-ttu-id="f94d9-236">Deze wijzigingen naar `app.js` opgeven dat de aanroepende code en de API aangeroepen zich in dezelfde Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f94d9-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span></span>
7. <span data-ttu-id="f94d9-237">Open de *app/scripts/homeCtrl.js* bestand.</span><span class="sxs-lookup"><span data-stu-id="f94d9-237">Open the *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="f94d9-238">Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.</span><span class="sxs-lookup"><span data-stu-id="f94d9-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="f94d9-239">Open de *app/scripts/indexCtrl.js* bestand.</span><span class="sxs-lookup"><span data-stu-id="f94d9-239">Open the *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="f94d9-240">Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.</span><span class="sxs-lookup"><span data-stu-id="f94d9-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>

### <a name="deploy-the-todolistangular-project-to-azure"></a><span data-ttu-id="f94d9-241">Het project ToDoListAngular implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f94d9-241">Deploy the ToDoListAngular project to Azure</span></span>
1. <span data-ttu-id="f94d9-242">Klik in **Solution Explorer** met de rechtermuisknop op het project ToDoListAngular. Klik vervolgens op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f94d9-243">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="f94d9-244">Visual Studio implementeert het project en opent een browservenster met de basis-URL van de web-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="f94d9-245">Hier ziet een fout 403-pagina normaal voor een poging is om naar een Web-API basis-URL vanuit een browser.</span><span class="sxs-lookup"><span data-stu-id="f94d9-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="f94d9-246">U hebt nog wel een wijziging aanbrengt in de middelste laag API-app voordat u kunt de toepassing testen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-246">You still have to make a change to the middle tier API app before you can test the application.</span></span>
3. <span data-ttu-id="f94d9-247">Sluit de browser.</span><span class="sxs-lookup"><span data-stu-id="f94d9-247">Close the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-use-authentication"></a><span data-ttu-id="f94d9-248">Configureren van het project ToDoListAPI om verificatie te gebruiken</span><span class="sxs-lookup"><span data-stu-id="f94d9-248">Configure the ToDoListAPI project to use authentication</span></span>
<span data-ttu-id="f94d9-249">Op dit moment het project ToDoListAPI verzendt ' * ' als de `owner` waarde ToDoListDataAPI.</span><span class="sxs-lookup"><span data-stu-id="f94d9-249">Currently the ToDoListAPI project sends "*" as the `owner` value to ToDoListDataAPI.</span></span> <span data-ttu-id="f94d9-250">In deze sectie kunt u de code voor het verzenden van de ID van de aangemelde gebruiker wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f94d9-250">In this section you change the code to send the ID of the logged-on user.</span></span>

<span data-ttu-id="f94d9-251">De volgende wijzigingen aanbrengen in het project ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="f94d9-251">Make the following changes in the ToDoListAPI project.</span></span>

1. <span data-ttu-id="f94d9-252">Open de *Controllers/ToDoListController.cs* bestand en het commentaar verwijderen van de regel in elke actiemethode voor de die wordt ingesteld `owner` met Azure AD `NameIdentifier` claimwaarde.</span><span class="sxs-lookup"><span data-stu-id="f94d9-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="f94d9-253">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f94d9-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="f94d9-254">**Belangrijke**: geen opmerkingen bij de code in de `ToDoListDataAPI` methode; doet u dat later voor de service principal verificatie zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f94d9-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span></span>

### <a name="deploy-the-todolistapi-project-to-azure"></a><span data-ttu-id="f94d9-255">Het project ToDoListAPI implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f94d9-255">Deploy the ToDoListAPI project to Azure</span></span>
1. <span data-ttu-id="f94d9-256">In **Solution Explorer**, met de rechtermuisknop op het project ToDoListAPI en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f94d9-257">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="f94d9-258">Visual Studio implementeert het project en opent een browservenster met de basis-URL van de API-app.</span><span class="sxs-lookup"><span data-stu-id="f94d9-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span></span>
3. <span data-ttu-id="f94d9-259">Sluit de browser.</span><span class="sxs-lookup"><span data-stu-id="f94d9-259">Close the browser.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="f94d9-260">De toepassing testen</span><span class="sxs-lookup"><span data-stu-id="f94d9-260">Test the application</span></span>
1. <span data-ttu-id="f94d9-261">Ga naar de URL van de web-app **met behulp van HTTPS niet HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="f94d9-262">Klik op de **To Do List** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f94d9-262">Click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="f94d9-263">U wordt gevraagd om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="f94d9-263">You are prompted to log in.</span></span>
3. <span data-ttu-id="f94d9-264">Aanmelden met de referenties van een gebruiker in uw AAD-tenant.</span><span class="sxs-lookup"><span data-stu-id="f94d9-264">Log in with the credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="f94d9-265">De **To Do List** pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f94d9-265">The **To Do List** page appears.</span></span>
   
   ![Takenlijstpagina](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="f94d9-267">Er is geen taakitems worden weergegeven omdat tot op heden alle eigenaar zijn ' * '.</span><span class="sxs-lookup"><span data-stu-id="f94d9-267">No to-do items are displayed because until now they have all been for owner "*".</span></span> <span data-ttu-id="f94d9-268">Nu de middelste laag items voor de aangemelde gebruiker vraagt en geen nog zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f94d9-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="f94d9-269">Toevoegen van nieuwe taakitems om te controleren of de toepassing werkt.</span><span class="sxs-lookup"><span data-stu-id="f94d9-269">Add new to-do items to verify that the application is working.</span></span>
6. <span data-ttu-id="f94d9-270">In een ander browservenster, Ga naar de Swagger-gebruikersinterface URL voor de ToDoListDataAPI-API-app en klik **ToDoList > ophalen**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="f94d9-271">Geef een sterretje voor de `owner` parameter en klik vervolgens op **Try it out in**.</span><span class="sxs-lookup"><span data-stu-id="f94d9-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="f94d9-272">Het antwoord ziet u dat de nieuwe taakitems de werkelijke hebben gebruikers-ID in de eigenschap Owner Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f94d9-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span></span>
   
   ![Eigenaar-ID in JSON-antwoord](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="f94d9-274">Het bouwen van de projecten maken</span><span class="sxs-lookup"><span data-stu-id="f94d9-274">Building the projects from scratch</span></span>
<span data-ttu-id="f94d9-275">De twee Web API-projecten zijn gemaakt met behulp van de **Azure API-App** project sjabloon en de waarden van standaard domeincontroller vervangen door een ToDoList-controller.</span><span class="sxs-lookup"><span data-stu-id="f94d9-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="f94d9-276">Zie voor meer informatie over het maken van een AngularJS-toepassing voor één pagina met een Web API 2 back-end [handen op Lab: bouwen van een enkele toepassing pagina WACHTWOORDVERIFICATIE met ASP.NET Web API en Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span><span class="sxs-lookup"><span data-stu-id="f94d9-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="f94d9-277">Zie de volgende bronnen voor meer informatie over het toevoegen van Azure AD verificatiecode op te geven:</span><span class="sxs-lookup"><span data-stu-id="f94d9-277">For information about how to add Azure AD authentication code, see the following resources:</span></span>

* <span data-ttu-id="f94d9-278">[Apps met Azure AD beveiligen AngularJS één pagina](../active-directory/active-directory-devquickstarts-angular.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="f94d9-279">Introductie van ADAL JS v1</span><span class="sxs-lookup"><span data-stu-id="f94d9-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="f94d9-280">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f94d9-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="f94d9-281">Zorg ervoor dat u en niet door elkaar ToDoListAPI (middelste laag) ToDoListDataAPI (gegevenslaag).</span><span class="sxs-lookup"><span data-stu-id="f94d9-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="f94d9-282">Controleer bijvoorbeeld of dat u verificatie toegevoegd aan de middelste laag API-app niet de gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="f94d9-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span></span> 
* <span data-ttu-id="f94d9-283">Zorg ervoor dat de broncode van de AngularJS verwijst naar de middelste laag API app-URL (ToDoListAPI, niet ToDoListDataAPI) en de juiste Azure AD-client-ID.</span><span class="sxs-lookup"><span data-stu-id="f94d9-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f94d9-284">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f94d9-284">Next steps</span></span>
<span data-ttu-id="f94d9-285">In deze zelfstudie hebt u geleerd hoe u App Service-verificatie voor een API-app en het aanroepen van de API-app met behulp van de ADAL-JS library.</span><span class="sxs-lookup"><span data-stu-id="f94d9-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span></span> <span data-ttu-id="f94d9-286">In de volgende zelfstudie leert u hoe u [beveiligde toegang tot uw API-app voor scenario's voor service to service](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="f94d9-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>

