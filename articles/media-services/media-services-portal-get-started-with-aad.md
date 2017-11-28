---
title: aaaGet gestart met Azure AD-verificatie met behulp van hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) verificatie tooconsume hello Azure Media Services-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="8c37d-103">Aan de slag met Azure AD-verificatie met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8c37d-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="8c37d-104">Meer informatie over hoe toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) verificatie tooaccess hello Azure Media Services-API.</span><span class="sxs-lookup"><span data-stu-id="8c37d-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c37d-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c37d-105">Prerequisites</span></span>

- <span data-ttu-id="8c37d-106">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8c37d-106">An Azure account.</span></span> <span data-ttu-id="8c37d-107">Als u geen account hebt, beginnen met een [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c37d-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="8c37d-108">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="8c37d-108">A Media Services account.</span></span> <span data-ttu-id="8c37d-109">Zie voor meer informatie [een Azure Media Services-account maken met behulp van Azure-portal Hallo](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="8c37d-110">Zorg ervoor dat u bekijkt hello [toegang tot Azure Media Services-API met Azure AD authentication overzicht](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="8c37d-111">Wanneer u Azure AD-verificatie met Azure Media Services gebruikt, hebt u twee opties voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="8c37d-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="8c37d-112">**Gebruikersverificatie**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-112">**User authentication**.</span></span> <span data-ttu-id="8c37d-113">Verifiëren van een persoon met Hallo app toointeract met Media Services-resources.</span><span class="sxs-lookup"><span data-stu-id="8c37d-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="8c37d-114">interactieve toepassing Hello moet eerst Hallo gebruiker gevraagd om referenties.</span><span class="sxs-lookup"><span data-stu-id="8c37d-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="8c37d-115">Een voorbeeld is van een management console-app gebruikt door gemachtigde gebruikers toomonitor codering taken of live te streamen.</span><span class="sxs-lookup"><span data-stu-id="8c37d-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="8c37d-116">**Verificatie van de service-principal**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-116">**Service principal authentication**.</span></span> <span data-ttu-id="8c37d-117">Een service verifiëren.</span><span class="sxs-lookup"><span data-stu-id="8c37d-117">Authenticate a service.</span></span> <span data-ttu-id="8c37d-118">Toepassingen die gebruikmaken van deze verificatiemethode vaak zijn apps die daemon-services, middelste laag services of geplande taken uitvoeren: web-apps, apps van de functie, logische apps, API's of een microservice.</span><span class="sxs-lookup"><span data-stu-id="8c37d-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c37d-119">Media Services ondersteunt momenteel hello Azure Access Control-servicemodel voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="8c37d-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="8c37d-120">Access Control-autorisatie wordt echter op 1 juni 2018 afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="8c37d-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="8c37d-121">U wordt aangeraden toohello Azure AD authentication model zo snel mogelijk te migreren.</span><span class="sxs-lookup"><span data-stu-id="8c37d-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="8c37d-122">Selecteer de verificatiemethode Hallo</span><span class="sxs-lookup"><span data-stu-id="8c37d-122">Select hello authentication method</span></span>

1. <span data-ttu-id="8c37d-123">In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="8c37d-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="8c37d-124">Selecteren hoe tooconnect toohello Media Services-API.</span><span class="sxs-lookup"><span data-stu-id="8c37d-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Selecteer op de pagina methode verbinding](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="8c37d-126">Gebruikersverificatie</span><span class="sxs-lookup"><span data-stu-id="8c37d-126">User authentication</span></span>

<span data-ttu-id="8c37d-127">tooconnect toohello Media Services-API met behulp van de optie voor verificatie van gebruiker hello, Hallo client-app moet toorequest een Azure AD-token heeft Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8c37d-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="8c37d-128">Azure AD-tenant-eindpunt</span><span class="sxs-lookup"><span data-stu-id="8c37d-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="8c37d-129">Media Services resource-URI</span><span class="sxs-lookup"><span data-stu-id="8c37d-129">Media Services resource URI</span></span>
* <span data-ttu-id="8c37d-130">Media Services (systeemeigen) toepassing client-ID</span><span class="sxs-lookup"><span data-stu-id="8c37d-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="8c37d-131">Media Services (systeemeigen)-toepassing omleidings-URI</span><span class="sxs-lookup"><span data-stu-id="8c37d-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="8c37d-132">Resource-URI voor de REST mediaservices</span><span class="sxs-lookup"><span data-stu-id="8c37d-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="8c37d-133">U kunt Hallo waarden ophalen voor deze parameters op Hallo **Media Services-API met gebruikersverificatie** pagina.</span><span class="sxs-lookup"><span data-stu-id="8c37d-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Verbinding maken met verificatie op de gebruikerspagina](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="8c37d-135">Als u verbinding toohello Media Services-API met behulp van Microsoft voor Media Services .NET SDK hello, vereist Hallo waarden zijn beschikbaar tooyou als onderdeel van Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="8c37d-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="8c37d-136">Zie voor meer informatie [met Azure AD authentication tooaccess hello Azure Media Services-API met .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="8c37d-137">Als u geen Hallo Media Services .NET SDK voor clients, moet u handmatig een Azure AD-tokenaanvraag maken met behulp van Hallo-parameters die eerder is besproken.</span><span class="sxs-lookup"><span data-stu-id="8c37d-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="8c37d-138">Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="8c37d-139">Verificatie van service-principal</span><span class="sxs-lookup"><span data-stu-id="8c37d-139">Service principal authentication</span></span>

<span data-ttu-id="8c37d-140">tooconnect toohello Media Services-API met behulp van service-principal optie Hallo, uw app middelste laag (web-API of webtoepassing) toorequest moet een Azure AD-token heeft Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="8c37d-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="8c37d-141">Azure AD-tenant-eindpunt</span><span class="sxs-lookup"><span data-stu-id="8c37d-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="8c37d-142">Media Services resource-URI</span><span class="sxs-lookup"><span data-stu-id="8c37d-142">Media Services resource URI</span></span> 
* <span data-ttu-id="8c37d-143">Resource-URI voor de REST mediaservices</span><span class="sxs-lookup"><span data-stu-id="8c37d-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="8c37d-144">Waarden van de toepassing Azure AD: Hallo **client-ID** en **clientgeheim**</span><span class="sxs-lookup"><span data-stu-id="8c37d-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="8c37d-145">U kunt Hallo waarden ophalen voor deze parameters op Hallo **tooMedia Services API verbinden met service-principal** pagina.</span><span class="sxs-lookup"><span data-stu-id="8c37d-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="8c37d-146">Gebruik deze pagina toocreate een nieuwe Azure AD-toepassing of tooselect een bestaande.</span><span class="sxs-lookup"><span data-stu-id="8c37d-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="8c37d-147">Nadat u hello Azure AD-app hebt geselecteerd, kunt u Haal Hallo client-ID (toepassings-ID) en Hallo client geheim (sleutel) waarden genereren.</span><span class="sxs-lookup"><span data-stu-id="8c37d-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Verbinding maken met de pagina van de service-principal](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="8c37d-149">Wanneer Hallo **Service-Principal** blade wordt geopend, Hallo eerste Azure AD-toepassing die voldoet aan de volgende criteria Hallo is ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="8c37d-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="8c37d-150">Het is een geregistreerde Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8c37d-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="8c37d-151">Het heeft Inzender of Owner Role-Based Access Control-machtigingen op Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="8c37d-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="8c37d-152">Nadat u maakt of een Azure AD-app selecteert, kunt u maken en een clientgeheim (sleutel) kopiëren en Hallo van client-ID (toepassings-ID).</span><span class="sxs-lookup"><span data-stu-id="8c37d-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="8c37d-153">Hallo client geheim en client-ID zijn vereiste tooget Hallo toegangstoken in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="8c37d-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="8c37d-154">Als u geen machtigingen toocreate Azure AD-apps in uw domein, hello Azure AD app besturingselementen van het Hallo-blade worden niet weergegeven en een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c37d-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="8c37d-155">Als u verbinding toohello Media Services-API met behulp van Media Services .NET SDK hello, Zie [met Azure AD authentication tooaccess hello Azure Media Services-API met .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="8c37d-156">Als u Media Services .NET SDK voor clients in Hallo niet gebruikt, moet u handmatig een tokenaanvraag van Azure AD met Hallo-parameters die eerder is besproken.</span><span class="sxs-lookup"><span data-stu-id="8c37d-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="8c37d-157">Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="8c37d-158">Hallo-client-ID en client geheim ophalen</span><span class="sxs-lookup"><span data-stu-id="8c37d-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="8c37d-159">Nadat u een bestaande Azure AD-app of selecteer Hallo optie toocreate een nieuwe selecteert, wordt Hallo knoppen volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8c37d-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Knop machtigingen en beheren toepassing knop beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="8c37d-161">tooopen hello blade van Azure AD-toepassing, klikt u op **beheren toepassing**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="8c37d-162">Op Hallo **beheren toepassing** blade, krijgt u Hallo-app client-ID (toepassings-ID).</span><span class="sxs-lookup"><span data-stu-id="8c37d-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="8c37d-163">een clientgeheim (sleutel), selecteer toogenerate **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Optie voor toepassing blade sleutels beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="8c37d-165">Machtigingen en de toepassing hello beheren</span><span class="sxs-lookup"><span data-stu-id="8c37d-165">Manage permissions and hello application</span></span>

<span data-ttu-id="8c37d-166">Nadat u Azure AD-toepassing hello selecteert, kunt u de toepassing hello en -machtigingen kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="8c37d-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="8c37d-167">tooset van uw Azure AD-toepassing tooaccess andere toepassingen, klikt u op **machtigingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="8c37d-168">Voor beheertaken, zoals het wijzigen van sleutels en antwoord-URL's of tooedit Hallo application manifest, klikt u op **beheren toepassing**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="8c37d-169">Hallo-app-instellingen bewerken of manifest</span><span class="sxs-lookup"><span data-stu-id="8c37d-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="8c37d-170">tooedit hello app-instellingen of manifest, klikt u op **beheren toepassing**.</span><span class="sxs-lookup"><span data-stu-id="8c37d-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Toepassingspagina beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="8c37d-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c37d-172">Next steps</span></span>

<span data-ttu-id="8c37d-173">Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="8c37d-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
