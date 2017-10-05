---
title: Native ClientApps - Azure AD publiceren | Microsoft Docs
description: Bevat informatie over het inschakelen van native client-apps om te communiceren met Azure AD Connector voor toepassingsproxy om te bieden veilige externe toegang tot uw lokale apps.
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
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="f1828-103">Native client-apps om te communiceren met de proxy toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="f1828-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="f1828-104">Naast de webtoepassingen, worden Azure Active Directory-toepassingsproxy ook gebruikt voor het publiceren van native client-apps.</span><span class="sxs-lookup"><span data-stu-id="f1828-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="f1828-105">Native client-apps verschillen van web-apps, omdat ze zijn geïnstalleerd op een apparaat, terwijl de web-apps via een browser worden geopend.</span><span class="sxs-lookup"><span data-stu-id="f1828-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="f1828-106">Toepassingsproxy ondersteunt native client-apps door overnemende Azure AD uitgegeven tokens die standaard autoriseren HTTP-headers zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="f1828-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relatie tussen eindgebruikers, Azure Active Directory en gepubliceerde toepassingen](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="f1828-108">Gebruik de Azure AD-Verificatiebibliotheek, die zorgt voor verificatie en biedt ondersteuning voor veel client-omgevingen, systeemeigen toepassingen te publiceren.</span><span class="sxs-lookup"><span data-stu-id="f1828-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="f1828-109">Toepassingsproxy in past de [systeemeigen toepassing aan Web-API-scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="f1828-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="f1828-110">Dit artikel begeleidt u bij de vier stappen voor het publiceren van een systeemeigen toepassing met toepassingsproxy en de Azure AD-Verificatiebibliotheek.</span><span class="sxs-lookup"><span data-stu-id="f1828-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="f1828-111">Stap 1: Uw toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="f1828-111">Step 1: Publish your application</span></span>
<span data-ttu-id="f1828-112">Uw proxy-toepassing te publiceren, net als alle andere toepassingen en gebruikers toegang krijgen tot uw toepassing toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="f1828-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="f1828-113">Zie voor meer informatie [publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f1828-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="f1828-114">Stap 2: Uw toepassing configureren</span><span class="sxs-lookup"><span data-stu-id="f1828-114">Step 2: Configure your application</span></span>
<span data-ttu-id="f1828-115">Uw eigen toepassing als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="f1828-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="f1828-116">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1828-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1828-117">Navigeer naar **Azure Active Directory** > **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="f1828-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="f1828-118">Selecteer **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="f1828-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="f1828-119">Geef een naam voor uw toepassing, selecteert **systeemeigen** als het toepassingstype, en geef de omleidings-URI voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1828-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Maak een nieuwe app-registratie](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="f1828-121">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f1828-121">Select **Create**.</span></span>

<span data-ttu-id="f1828-122">Zie voor meer informatie over het maken van een nieuwe app-registratie, [toepassingen integreren met Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f1828-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="f1828-123">Stap 3: Verleen toegang tot andere toepassingen</span><span class="sxs-lookup"><span data-stu-id="f1828-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="f1828-124">De systeemeigen toepassing worden blootgesteld aan andere toepassingen in uw directory inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f1828-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="f1828-125">Nog steeds in **App registraties**, selecteer de nieuwe systeemeigen toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1828-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="f1828-126">Selecteer **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="f1828-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="f1828-127">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f1828-127">Select **Add**.</span></span>
4. <span data-ttu-id="f1828-128">Open de eerste stap **selecteert u een API**.</span><span class="sxs-lookup"><span data-stu-id="f1828-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="f1828-129">Gebruik de zoekbalk de toepassingsproxy-app die u hebt gepubliceerd in de eerste sectie vinden.</span><span class="sxs-lookup"><span data-stu-id="f1828-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="f1828-130">Kies deze app en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f1828-130">Choose that app, then click **Select**.</span></span> 

   ![Zoeken naar de proxy-app](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="f1828-132">Open de tweede stap **machtigingen selecteren**.</span><span class="sxs-lookup"><span data-stu-id="f1828-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="f1828-133">Gebruik de selectievakjes om uw eigen App toegang verlenen tot uw proxy-toepassing en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f1828-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Toegang verlenen tot de proxy-app](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="f1828-135">Selecteer **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="f1828-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="f1828-136">Stap 4: De Active Directory Authentication Library bewerken</span><span class="sxs-lookup"><span data-stu-id="f1828-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="f1828-137">De systeemeigen toepassingscode bewerken in de verificatiecontext van de Active Directory Authentication Library (ADAL) om op te nemen van de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f1828-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="f1828-138">De variabelen in de voorbeeldcode wordt vervangen als volgt:</span><span class="sxs-lookup"><span data-stu-id="f1828-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="f1828-139">**Tenant-ID** vindt u in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f1828-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="f1828-140">Navigeer naar **Azure Active Directory** > **eigenschappen** en kopieer de map-ID.</span><span class="sxs-lookup"><span data-stu-id="f1828-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="f1828-141">**Externe URL** is de front-URL die u hebt ingevoerd in de Proxy-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1828-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="f1828-142">U vindt deze waarde, gaat u naar de **toepassingsproxy** sectie van de proxy-app.</span><span class="sxs-lookup"><span data-stu-id="f1828-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="f1828-143">**App-ID** van de systeemeigen app kunt u vinden op de **eigenschappen** pagina van de oorspronkelijke toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1828-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="f1828-144">**Omleidings-URI van de systeemeigen app** vindt u op de **omleidings-URI's** pagina van de oorspronkelijke toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1828-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="f1828-145">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f1828-145">See also</span></span>

<span data-ttu-id="f1828-146">Zie voor meer informatie over de stroom systeemeigen toepassing [systeemeigen toepassing aan web-API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="f1828-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="f1828-147">Ga naar het [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/) voor nieuws en updates.</span><span class="sxs-lookup"><span data-stu-id="f1828-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
