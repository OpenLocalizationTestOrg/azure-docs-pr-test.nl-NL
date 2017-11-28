---
title: aaaPublish native client-apps - Azure AD | Microsoft Docs
description: Bevat informatie over hoe tooenable native client-apps toocommunicate met Azure AD-Application Proxy Connector tooprovide veilige externe toegang tooyour lokale apps.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="f5a63-103">Hoe tooenable native client-apps toointeract met proxy toepassingen</span><span class="sxs-lookup"><span data-stu-id="f5a63-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="f5a63-104">Azure Active Directory-toepassingsproxy kan toevoeging tooweb toepassingen, ook gebruikte toopublish native client-apps worden.</span><span class="sxs-lookup"><span data-stu-id="f5a63-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="f5a63-105">Native client-apps verschillen van web-apps, omdat ze zijn geïnstalleerd op een apparaat, terwijl de web-apps via een browser worden geopend.</span><span class="sxs-lookup"><span data-stu-id="f5a63-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="f5a63-106">Toepassingsproxy ondersteunt native client-apps door overnemende Azure AD uitgegeven tokens die standaard autoriseren HTTP-headers zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="f5a63-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relatie tussen eindgebruikers, Azure Active Directory en gepubliceerde toepassingen](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="f5a63-108">Hello Azure AD-Verificatiebibliotheek, die zorgt voor verificatie en biedt ondersteuning voor veel client omgevingen, toopublish systeemeigen toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f5a63-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="f5a63-109">Toepassingsproxy in Hallo past [systeemeigen toepassing tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="f5a63-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="f5a63-110">Dit artikel begeleidt u bij Hallo vier stappen toopublish een systeemeigen toepassing met toepassingsproxy en hello Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="f5a63-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="f5a63-111">Stap 1: Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="f5a63-111">Step 1: Publish your application</span></span>
<span data-ttu-id="f5a63-112">Uw proxy-toepassing te publiceren, net als elke andere toepassing en toewijzen van gebruikers tooaccess uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5a63-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="f5a63-113">Zie voor meer informatie [publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f5a63-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="f5a63-114">Stap 2: Uw toepassing configureren</span><span class="sxs-lookup"><span data-stu-id="f5a63-114">Step 2: Configure your application</span></span>
<span data-ttu-id="f5a63-115">Uw eigen toepassing als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="f5a63-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="f5a63-116">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f5a63-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5a63-117">Navigeer te**Azure Active Directory** > **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="f5a63-118">Selecteer **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="f5a63-119">Geef een naam voor uw toepassing, selecteert **systeemeigen** als het toepassingstype hello, en geef Hallo omleidings-URI voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5a63-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Maak een nieuwe app-registratie](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="f5a63-121">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-121">Select **Create**.</span></span>

<span data-ttu-id="f5a63-122">Zie voor meer informatie over het maken van een nieuwe app-registratie, [toepassingen integreren met Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f5a63-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="f5a63-123">Stap 3: Verlenen toegang tooother toepassingen</span><span class="sxs-lookup"><span data-stu-id="f5a63-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="f5a63-124">Hallo systeemeigen toepassing toobe blootgesteld tooother toepassingen in uw directory inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f5a63-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="f5a63-125">Nog steeds in **App registraties**, selecteer Hallo nieuwe systeemeigen toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f5a63-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="f5a63-126">Selecteer **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="f5a63-127">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-127">Select **Add**.</span></span>
4. <span data-ttu-id="f5a63-128">Eerste stap van de Open Hallo **selecteert u een API**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="f5a63-129">Hallo zoeken balk toofind Hallo toepassingsproxy app gebruiken die u hebt gepubliceerd in de eerste sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f5a63-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="f5a63-130">Kies deze app en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-130">Choose that app, then click **Select**.</span></span> 

   ![Zoeken naar Hallo proxy app](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="f5a63-132">Tweede stap van de Open Hallo **machtigingen selecteren**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="f5a63-133">Hallo selectievakje toogrant uw toepassing systeemeigen toepassing toegang tooyour proxy gebruiken en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Verleen toegang tooproxy app](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="f5a63-135">Selecteer **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="f5a63-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="f5a63-136">Stap 4: Hallo Active Directory Authentication Library bewerken</span><span class="sxs-lookup"><span data-stu-id="f5a63-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="f5a63-137">Hallo systeemeigen toepassingscode bewerken in Hallo authentication context Hallo Active Directory Authentication Library (ADAL) tooinclude Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f5a63-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="f5a63-138">Hallo variabelen in de voorbeeldcode hello wordt vervangen als volgt:</span><span class="sxs-lookup"><span data-stu-id="f5a63-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="f5a63-139">**Tenant-ID** vindt u in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f5a63-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="f5a63-140">Navigeer te**Azure Active Directory** > **eigenschappen** en kopiëren Hallo Directory-ID.</span><span class="sxs-lookup"><span data-stu-id="f5a63-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="f5a63-141">**Externe URL** Hallo front-URL die u hebt ingevoerd in de Proxy-toepassing hello is.</span><span class="sxs-lookup"><span data-stu-id="f5a63-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="f5a63-142">toofind dit waarde, navigeer toohello **toepassingsproxy** sectie van Hallo proxy app.</span><span class="sxs-lookup"><span data-stu-id="f5a63-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="f5a63-143">**App-ID** Hallo systeemeigen app vindt u op Hallo **eigenschappen** pagina van de systeemeigen toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="f5a63-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="f5a63-144">**Omleidings-URI van de systeemeigen app Hallo** vindt u op Hallo **omleidings-URI's** pagina van de systeemeigen toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="f5a63-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="f5a63-145">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f5a63-145">See also</span></span>

<span data-ttu-id="f5a63-146">Zie voor meer informatie over Hallo systeemeigen toepassing stroom [systeemeigen toepassing tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="f5a63-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="f5a63-147">Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="f5a63-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
